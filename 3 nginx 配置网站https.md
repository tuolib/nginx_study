### 查看端口占用
- yum -y install net-tools
- netstat -ntlp

### nginx 配置 vue 前端

- nginx 配置中不要有中文
- 域名 https://test.connorfree.ml
- 假设 前端打包文件放的地址为 /var/www/html/h5_1, 这个文件夹下有index.html

```
location / {
    # 前端文件路径
    root  /var/www/html/h5_1;
    #hash模式只配置访问html就可以了
    index  index.html; 
    # history模式下
    try_files $uri $uri/ /index.html;
}
```

- 正常以上就可以了。如果说history 路由下，假设有如下路径 https://test.connorfree.ml/m  , 加个 /m 访问移动端html，再加如下配置，且前端代码中， history 路由配置的 BASE_URL 要变成 ‘m’, 

```
location /m { 
    # 子级目录
    alias  /var/www/html/m;
    index  index.html;
    try_files $uri $uri/ /m/index.html; 
}
```

### firewalld
```
systemctl disable firewalld
systemctl stop firewalld
systemctl status firewalld

```

### 校验配置是否正确

```
nginx -t -c /etc/nginx/nginx.conf
```



### nginx 配置 websocket

- 文档地址 https://www.nginx.com/blog/websocket-nginx/

- 本文假设
> 网站域名为： https://test.connorfree.ml，

> 后端服务器nodejs api 启动端口 localhost:3000, 

> websocket 服务器启动端口为 localhost:45389

> js 连接 websocket 地址为 https://test.connorfree.ml/wsapp



- 那么 nginx 中需要加入如下配置

```
map $http_upgrade $connection_upgrade {
    default upgrade;
    '' close;
}

upstream wsbackend {
    server localhost:45389;
}

location /wsapp/ {
    # 此句含义是：前端连接 https://test.connorfree.ml/wsapp，
    # 那么会转到本地 upstream wsbackend
    proxy_pass http://wsbackend;
    proxy_http_version 1.1;
    proxy_set_header Upgrade $http_upgrade;
    proxy_set_header Connection "Upgrade";
    proxy_set_header Host $host;
}
```