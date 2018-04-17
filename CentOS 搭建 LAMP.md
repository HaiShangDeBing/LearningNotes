# CentOS 搭建 LAMP

## 搭建 MySQL 数据库

使用 `yum` 安装 MySQL：

```
yum install mysql-server -y
```

安装完成后，启动 MySQL 服务：

```
service mysqld restart
```

设置 MySQL 账户 root 密码：

```
/usr/bin/mysqladmin -u root password 'fkSCUEyI'
```

## 安装 Apache 服务

使用 `yum` 安装 Apache

```
yum install httpd -y
```

启动 Apache 服务：

```
service httpd start
```

## 安装 PHP 和 PHP-MySQL 支持工具

 使用 `yum` 安装 PHP：

```
yum install php php-mysql -y
```

## 检验是否安装成功

我们在 [/var/www/html]() 目录下创建一个info.php文件来检查php是否安装成功，示例代码参考如下info.php

```
<?php phpinfo(); ?>
```

重启 Apache 服务：

```
service httpd restart
```

此时，访问 [http://119.29.226.77/info.php]() 可浏览到我们刚刚创建的 info.php 页面了。

## CentOS 配置 apache 的 https 服务

1. 向证书机构申请https证书或者使用openssl配置生成，会得到xxx.crt和xxx.key。
2. 安装apache的mod_ssl.so模块

```
yum -y install mod_ssl
```

3. 修改 /etc/httpd/conf.d/ssl.conf

```
vim /etc/httpd/conf.d/ssl.conf
 
DocumentRoot "/var/www/html/test"
ServerName wxapp.peopleyuqing.com:443
SSLCertificateFile /etc/pki/tls/certs/xxx.crt    //需要把xxx.crt放到该路径下或另起路径，下同
SSLCertificateKeyFile /etc/pki/tls/private/xxx.key
```

4. 修改 /etc/httpd/conf/httpd.conf

```
vim /etc/httpd/conf/httpd.conf
加载mod_ssl.so模块LoadModule ssl_module modules/mod_ssl.so
加载ssl.conf文件Include conf.d/*.conf（或者Include conf.d/ssl.conf）
```

5. 测试配置文件并重启apache

```
sudo httpd -t (或者sudo service httpd configtest)
sudo service httpd restart
```

6. 在刚才指定的根目录下生成php测试文件用于验证https域名是否配置成功。