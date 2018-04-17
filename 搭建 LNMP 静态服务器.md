# 搭建 LNMP 静态服务器

## 安装 Nginx

使用 `yum` 安装 Nginx：

```
yum install nginx -y
```

修改/etc/nginx/conf.d/default.conf，去除对 IPv6 地址的监听，CentOS 6 不支持 IPv6，需要取消对 IPv6 地址的监听，否则 Nginx 不能成功启动。

```
server {
    listen       80 default_server;
    # listen       [::]:80 default_server;
    server_name  _;
    root         /usr/share/nginx/html;

    # Load configuration files for the default server block.
    include /etc/nginx/default.d/*.conf;

    location / {
    }

    error_page 404 /404.html;
        location = /40x.html {
    }

    error_page 500 502 503 504 /50x.html;
        location = /50x.html {
    }

}
```

修改完成后，启动 Nginx：

```
nginx
```

此时，可访问实验机器外网 HTTP 服务（[http://xxx.xxx.xxx.xxx]()）来确认是否已经安装成功。

将 Nginx 设置为开机自动启动：

```
chkconfig nginx on
```

## 安装 MySQL

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
/usr/bin/mysqladmin -u root password 'VsoUWMsv'
```

将 MySQL 设置为开机自动启动：

```
chkconfig mysqld on
```

## 安装 PHP

 使用`yum`安装 PHP：

```
yum install php php-fpm php-mysql -y
```

安装之后，启动 PHP-FPM 进程：

```
service php-fpm start
```

启动之后，可以使用下面的命令查看 PHP-FPM 进程监听哪个端口

```
netstat -nlpt | grep php-fpm
```

把 PHP-FPM 也设置成开机自动启动：

```
chkconfig php-fpm on
```
## 配置 Nginx 并运行 PHP 程序

在 [/etc/nginx/conf.d]() 目录中新建一个名为 php.conf 的文件，并配置 Nginx 端口 ，配置示例如下：

```
server {
    listen 8000;
    # pass the PHP scripts to FastCGI server listening on 127.0.0.1:9000
    location ~ .php$ {
        root           /usr/share/php;
        fastcgi_pass   127.0.0.1:9000;
        fastcgi_index  index.php;
        fastcgi_param  SCRIPT_FILENAME  $document_root$fastcgi_script_name;
        include        fastcgi_params;
    }
}
```

修改配置完成后，重启 nginx 服务

```
 service nginx restart
```

这时候，我们就可以在[/usr/share/php]() 目录下新建一个 info.php 文件来检查 php 是否安装成功了，文件内容参考如下：

```
<?php phpinfo(); ?>
```

此时，访问 [http://xxx.xxx.xxx.xxx:8000/info.php]() 可浏览到我们刚刚创建的 info.php 页面了。

## Nginx 常用命令

```
nginx -s reload 重新加载
nginx -c xxx.conf 选择某conf文件加载
nginx -t -c xxx.conf 看某conf文件是否配置正确
ps -ef|grep nginx 查看nginx进程
pkill -9 nginx 杀死全部nginx进程
```

