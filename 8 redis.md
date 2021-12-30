```

sudo yum install epel-release yum-utils
sudo yum install http://rpms.remirepo.net/enterprise/remi-release-7.rpm
sudo yum-config-manager --enable remi

yum install redis

systemctl start redis
systemctl enable redis
systemctl status redis
systemctl restart redis


sudo firewall-cmd --new-zone=redis --permanent
sudo firewall-cmd --zone=redis --add-port=6379/tcp --permanent
sudo firewall-cmd --zone=redis --add-source=192.168.121.0/24 --permanent
sudo firewall-cmd --reload

```

