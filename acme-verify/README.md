## 简介

某奇怪的搭配`acme.sh`等使用的`http`验证签发证书需求

## 用法
```
# 创建一个 Docker 卷，用于持久化 acme-verify 的数据
docker volume create acme-verify-data

# 运行一个 acme-verify 容器，映射 80 端口，使用 acme-verify-data 卷，并设置 NGINX_DOMAIN 环境变量
docker run -d \
    --name acme-verify \
    --restart unless-stopped \
    -p 80:80 \
    -v acme-verify-data:/usr/share/nginx/html \
    -e NGINX_DOMAIN=domain.com \
    moelin/acme-verify:latest
```

```
# 使用 acme.sh 进行证书签发，指定域名 domain.com 和验证路径 /var/lib/docker/volumes/acme-verify-data/_data
acme.sh --issue -d domain.com -w /var/lib/docker/volumes/acme-verify-data/_data
```