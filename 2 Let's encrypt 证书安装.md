### 购买域名

- 购买服务器，

- 购买免费域名  https://www.freenom.com/zh/index.html?lang=zh

- 购买方法 网上搜索，并在这个网站上 将服务器 IP 解析到域名下才能安装 let's encrypt

- 本文以 test.connorfree.ml 域名为例
 
### 登录服务器

- 使用工具

- mac: sftp 传输文件工具：FileZilla; 命令行工具：自带终端就可以连接服务器
- windows: sftp 传输文件工具: winScp; 命令行工具：xshell

### 方法1 cerbot-auto 安装 

```
cd /usr/local/bin
wget https://dl.eff.org/certbot-auto
chmod a+x certbot-auto
./certbot-auto

```

ssl_trusted_certificate /etc/letsencrypt/live/example.com/chain.pem;

### 方法2 使用acme 安装 

```
yum install socat

curl  https://get.acme.sh | sh

# 更新命令，就可以直接使用 acme.sh 命令行
source .bash_profile

# 生成证书
acme.sh --issue -d test.connorfree.ml --standalone -k ec-256

# 手动更新证书 
acme.sh --renew -d mydomain.com --force --ecc



# 创建/root/v2r文件夹，并安装证书至此路径下：
mkdir /root/v2r

acme.sh  --ecc --installcert -d test.connorfree.ml --key-file /root/v2r/test.connorfree.ml.key --fullchain-file /root/v2r/test.connorfree.ml.cer

# 自动更新证书
acme.sh --upgrade --auto-upgrade
```

### 方法3 cerbot 安装 

```
yum install epel-release

yum update

yum install nginx

systemctl start nginx

yum install certbot python2-certbot-nginx


certbot --nginx -d test.connorfree.ml



```

- nginx 添加证书文件地址， 例子如当前文件夹 nginx.conf

```

ssl_certificate "/etc/letsencrypt/live/test.connorfree.ml/fullchain.pem";
ssl_certificate_key "/etc/letsencrypt/live/test.connorfree.ml/privkey.pem";

```


### 方法4 cerbot-auto 安装 
https://xieyonghui.com/tech/lets-encrypt_181.html

```
 wget https://dl.eff.org/certbot-auto

 chmod a+x ./certbot-auto

 ./certbot-auto --nginx

```



