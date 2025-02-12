# conf.d

```bash
server {
  listen 80;
  server_name dev.local; # localhost domain

  index index.html index.htm;
  add_header 'Access-Control-Expose-Headers' 'APP-VERSION';

  # frontend
  location ^~ / {
    proxy_pass http://host.docker.internal:3000;
    proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
    proxy_set_header Host $http_host;
    proxy_set_header X-Forwarded-Proto $scheme;
    proxy_redirect off;
  }

  # backend
  location ^~ /dashboard {
    proxy_pass http://host.docker.internal:8098;
    proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
    proxy_set_header Host $http_host;
    proxy_set_header X-Forwarded-Proto $scheme;
    proxy_redirect off;
  }
}
```

## etc/hosts

```txt
# 本地开发项目地址
127.0.0.1 dev.local

# Added by Docker Desktop
192.168.1.* host.docker.internal #eg: 192.168.1.10
192.168.1.* gateway.docker.internal
```
