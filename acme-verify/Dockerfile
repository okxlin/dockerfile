# 使用官方 Nginx 镜像作为基础镜像
FROM nginx:stable-alpine-slim

# 复制自定义的 Nginx 配置文件到容器内部
COPY nginx.conf /etc/nginx/nginx.conf

# 设置默认环境变量
ENV NGINX_DOMAIN example.com

# 在容器启动时执行的命令
CMD sed -i "s/{{DOMAIN}}/$NGINX_DOMAIN/g" /etc/nginx/nginx.conf && nginx -g 'daemon off;'

# 暴露容器的 80 端口
EXPOSE 80
