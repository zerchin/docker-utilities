1. 首先新建一个存放配置的目录

```
cd ~
mkdir headscale
cd headscale
mkdir -p {nginx,nginx/ssl,config,lib,run}
```

2. 接着在 nginx 目录下，配置 `nginx.conf`文件，在 nginx/ssl 目录下，存放证书文件，如下：

```
# ls nginx/*
nginx/nginx.conf

nginx/ssl:
tls.crt  tls.key
```

3. 在 config 目录下，配置 headscale 的 config.yaml 文件，修改如下几个配置：
```yaml
## 访问的域名
server_url: https://<domain_name>

## API 监听端口
listen_addr: 0.0.0.0:8080

## 
grpc_listen_addr: 0.0.0.0:50443

## 根据查询到的资料，建议打开随机端口，否则可能会出现连接不稳定的问题
randomize_client_port: true

## 自定义子网，如果跟现有网段不冲突，可以不修改
prefixes:
  v4: 100.64.0.0/10
```
4. 启动
```bash
docker-compose up -d
```
