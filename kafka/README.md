# Kafka

## Manually Create a Topic for bitnami/kafka

```bash
docker exec -it kafka bash
```

## Create a Topic

```bash
docker exec -it kafka bash
/opt/bitnami/kafka/bin/kafka-topics.sh --create --topic spider.productlist --bootstrap-server localhost:9092 --replication-factor 1 --partitions 3
exit
```

## List Topics

```bash
docker exec -it kafka bash
/opt/bitnami/kafka/bin/kafka-topics.sh --list --bootstrap-server localhost:9092
exit
```

## Delete Topics

```bash
docker exec -it kafka bash
/opt/bitnami/kafka/bin/kafka-topics.sh --delete --topic spider.productlist --bootstrap-server localhost:9092
exit
```
