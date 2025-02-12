# 备份时忽略所有者

```bash
pg_dump -U username -d dbname -O --no-acl --no-owner -f backup_file.sql
```

## 还原

```bash
psql -U username -d dbname -f backup_file.sql
```

## 备份单/多表

```bash
pg_dump -U username -d dbname -O --no-acl --no-owner -t table1 -t table2 -f backup_tables.sql
```

## 还原单/多表

```bash
psql -U username -d dbname -f backup_tables.sql
```

## 还原时重置序列[单表]

```bash
SELECT pg_catalog.setval(pg_get_serial_sequence('tablename', 'id'), MAX(id)) FROM tablename;
```

## 使用 SQL 脚本自动化重置序列

```bash
DO $$
DECLARE
    table_name TEXT;
    column_exists BOOLEAN;
    sequence_name TEXT;
    max_id INT;
BEGIN
    -- 遍历所有表
    FOR table_name IN
        SELECT tablename
        FROM pg_tables
        WHERE schemaname = 'public' -- 假设表在 public 模式中
    LOOP
        -- 检查“id”列是否存在
        EXECUTE format('
            SELECT EXISTS (
                SELECT 1
                FROM information_schema.columns
                WHERE table_name = %L AND column_name = ''id''
            )', table_name) INTO column_exists;

        -- 如果“id”列存在
        IF column_exists THEN
            -- 获取表的序列名称
            sequence_name := pg_get_serial_sequence(table_name, 'id'); -- 假设主键列名为 'id'

            -- 如果表有序列
            IF sequence_name IS NOT NULL THEN
                -- 获取当前表的最大 ID
                EXECUTE 'SELECT COALESCE(MAX(id), 0) FROM ' || table_name INTO max_id;

                IF max_id > 0 THEN
                    -- 重置序列
                    EXECUTE 'SELECT setval(''' || sequence_name || ''', ' || max_id || ')';

                    -- 打印日志
                    RAISE NOTICE 'Reset sequence % for table % to %', sequence_name, table_name, max_id;
                ELSE
                    -- 打印日志，跳过重置
                    RAISE NOTICE 'Skipping sequence reset for table % due to max_id being 0', table_name;
                END IF;
            END IF;
        ELSE
            -- 如果“id”列不存在，打印日志
            RAISE NOTICE 'Table: %, Does not have "id"', table_name;
        END IF;
    END LOOP;
END $$;
```

## 用 cron 作业

```bash
0 2 * * * /usr/bin/pg_dump -U username -d dbname -f /path/to/backup/backup_$(date +\%Y\%m\%d).sql
```

## 查看所有表（包括模式）

```bash
\dt
```

## 清屏

```bash
\! clear
\! cls
```

## 删除 public 模式下的所有表

```bash
DO $$
DECLARE
    r RECORD;
BEGIN
    FOR r IN (SELECT tablename FROM pg_tables WHERE schemaname = 'public')
    LOOP
        EXECUTE 'DROP TABLE IF EXISTS public.' || quote_ident(r.tablename) || ' CASCADE';
    END LOOP;
END $$;
```
