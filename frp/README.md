#### frps 服务端设置 [debian12]

在 github 上[frp](https://github.com/fatedier/frp)下载 releases 最新版本。

解压 到 /usr/local/frps

配置文件 /usr/local/frps/frps.toml

系统服务 frps.service

启动服务 systemctl [start|enable] frps

### nginx 配置ssl域名，比如微信公众号开发，需要配置

```conf
  # frps 代理
  location ^~ / {
      proxy_pass http://127.0.0.1:5480;  # 转发到的地址和端口
      proxy_set_header   Host             $host;
      proxy_set_header   X-Real-IP        $remote_addr;
      proxy_set_header   X-Forwarded-For  $proxy_add_x_forwarded_for;
  }

  location ^~ /dashboard {
      proxy_pass http://127.0.0.1:6443;  # 转发到的地址和端口
      proxy_set_header   Host             $host;
      proxy_set_header   X-Real-IP        $remote_addr;
      proxy_set_header   X-Forwarded-For  $proxy_add_x_forwarded_for;
  }
```

#### frpc 客户端设置 [windows11]
