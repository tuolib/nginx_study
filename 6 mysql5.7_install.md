## mysql 5.7 安装

- 添加Mysql5.7仓库
```
sudo rpm -ivh https://dev.mysql.com/get/mysql57-community-release-el7-11.noarch.rpm
```

- 确认Mysql仓库成功添加
```
yum repolist all | grep mysql | grep enabled
```

- 开始安装Mysql5.7
```
yum -y install mysql-community-server
```


- 启动Mysql
- 启动
```
systemctl start mysqld
```

- 设置系统启动时自动启动
```
systemctl enable mysqld
```

- 查看启动状态
```
systemctl status mysqld
```

- Mysql的安全设置
CentOS上的root默认密码可以在文件/var/log/mysqld.log找到，通过下面命令可以打印出来
```
cat /var/log/mysqld.log | grep -i 'temporary password'
```
执行下面命令进行安全设置，这个命令会进行设置root密码设置，移除匿名用户，禁止root用户远程连接等
```
mysql_secure_installation
```

- 设置数据库编码为utf8

- 打开配置文件

```
vi /etc/my.cnf
```

- 在[mysqld]，[client]，[mysql]节点下添加编码设置

```shell
[client]
default-character-set=utf8mb4

[mysql]
default-character-set=utf8mb4

[mysqld]
collation-server = utf8mb4_unicode_ci
character-set-client-handshake = FALSE
character-set-server = utf8mb4
init-connect='SET NAMES utf8mb4'
```

- 重启Mysql即可


- 允许远程连接mysql
```
GRANT ALL PRIVILEGES ON *.* TO 'root'@'%' IDENTIFIED BY 'Hello123!' WITH GRANT OPTION;
FLUSH PRIVILEGES;

```


pdh,XfoPk3TP
