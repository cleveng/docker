### docker for mac/windows/linux 本地开发环境

### docker proxy config

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

### database config for mysql,mssql,redis,mongo,postgresql
username: root
password: secret
