# docker for mac/windows/linux 本地开发环境

## docker proxy config

edit `${home}/.docker/config.json`

```json
{
  "proxies": {
    "default": {
      "httpProxy": "http://proxy.example.com:3128",
      "httpsProxy": "https://proxy.example.com:3129",
      "noProxy": "*.test.example.com,.example.org,127.0.0.0/8"
    }
  }
}
```

## database config for mysql,mssql,redis,mongo,postgresql

username: root
password: secret

## git proxy

```bash
git config --global user.name "Your Name"
git config --global user.email "your_email@example.com"
git config --global http.proxy http://username:password@proxyserver:port
git config --global https.proxy https://username:password@proxyserver:port

git config --global --list

export HTTP_PROXY=http://username:password@proxyserver:port
export HTTPS_PROXY=http://username:password@proxyserver:port
```

## docker 配置

```bash
cat > /etc/docker/daemon.json << EOF
{
    "log-driver": "json-file",
    "log-opts": {
        "max-size": "20m",
        "max-file": "3"
    },
    "ipv6": true,
    "fixed-cidr-v6": "fd00:dead:beef:c0::/80",
    "experimental":true,
    "ip6tables":true
}
EOF
```
