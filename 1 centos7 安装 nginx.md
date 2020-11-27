

### 方法1 安装最新版本

- Configure Nginx Repo

Run this command:
```
vi /etc/yum.repos.d/nginx.repo

```

Now copy and paste this code to nginx.repo file (SHIFT+INS):

```
[nginx]
name=nginx repo
baseurl=http://nginx.org/packages/mainline/centos/7/$basearch/
gpgcheck=0

```

- Install Nginx

```
# Run this command to install Nginx:
yum install nginx

# Start Nginx server:
systemctl start nginx

# Enable Nginx to start at boot:
systemctl enable nginx

```

- Useful Commands

```
sudo systemctl stop nginx
sudo systemctl restart nginx
sudo systemctl status nginx

```

- Advanced (Firewall)
```
sudo firewall-cmd --permanent --zone=public --add-service=http 
sudo firewall-cmd --permanent --zone=public --add-service=https
sudo firewall-cmd --reload

```

### 方法1 使用 yum 安装

- 使用网站中的 yum 安装 https://juejin.im/post/6844904134345228301


- https://www.mynotepaper.com/install-nginx-on-centos-7



### 常见错误

- 403 forbidden

```

# 前端打包文件夹给权限
chmod 755  /var/www/*
restorecon -r /var/www/html
chown  -R  nginx:nginx /var/www/html
chcon -R -t httpd_sys_content_t
```

- 502 bad gateway

```
setsebool -P httpd_can_network_connect 1

```

