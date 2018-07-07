# 基于showdoc搭建的CNJS后端API在线文档
特别感谢开源的showdoc文档
## 0、服务器系统环境
centos7
## 1、准备 Nginx + PHP 环境
### 安装 Nginx
```
yum install nginx
```
### 配置Nginx
修改 `/etc/nginx/nginx.conf` 文件，将`server`对应字段替换或添加如下内容：
```
    server {
        listen       80 default_server;
        listen       [::]:80 default_server;
        server_name  0.0.0.0;
        root         /var/www/html/apidoc;
        index index.php index.html

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
        location ~ .php$ {
            root           /var/www/html/apidoc;
            fastcgi_pass   127.0.0.1:9000;
            fastcgi_index  index.php;
            fastcgi_param  SCRIPT_FILENAME  $document_root$fastcgi_script_name;
            include        fastcgi_params;
        }
        location ~ /.ht {
            deny  all;
        }
    }
```
### 启动 Nginx 并设置为开机启动：
```
service nginx start
chkconfig nginx on
```
### 安装 PHP
```
yum install php php-gd php-fpm php-mcrypt php-mbstring php-mysql php-pdo
```
### 启动 php-fpm 并设置为开机启动：
```
service php-fpm start
chkconfig php-fpm on
```

## 2、安装配置apidoc
### 获取源文件
```
git clone https://github.com/cn-js/api
```
### 配置apidoc
1. 移动`api/apidoc`文件夹到`/var/www/html`目录中
2. 设置 apidoc 目录写权限
```
chmod a+w apidoc/install
chmod a+w apidoc/Sqlite
chmod a+w apidoc/Sqlite/showdoc.db.php
chmod a+w apidoc/Public/Uploads/
chmod a+w apidoc/Application/Runtime
chmod a+w apidoc/server/Application/Runtime
chmod a+w apidoc/Application/Common/Conf/config.php
chmod a+w apidoc/Application/Home/Conf/config.php
```

## 大功告成
现在可以通过浏览器访问`http://<您的IP地址>/web/#/1`来查看API文档了