### 基于Ubuntu系统的Apache服务器的多站点配置

#### 1.修改文件/etc/apache2/sites-available/000-default.conf(相当于本地wamp\bin\apache\apache2.4.18\conf\extra\httpd-vhosts.conf)，设置不同的ServerName、DocumentRoot 和 Directory 

```
<VirtualHost *:80>
   ServerAdmin webmaster1@localhost
   DocumentRoot 项目路径1
   ServerName www.aaa.com

   <Directory 项目路径1>
   Options Indexes FollowSymLinks
   AllowOverride All
   Require all granted
   </Directory>

   ErrorLog ${APACHE_LOG_DIR}/error.log
   CustomLog ${APACHE_LOG_DIR}/access.log combined
</VirtualHost>
```

```
<VirtualHost *:80>
   ServerAdmin webmaster1@localhost
   DocumentRoot 项目路径2
   ServerName www.bbb.com

   <Directory 项目路径2>
   Options Indexes FollowSymLinks
   AllowOverride All
   Require all granted
   </Directory>

   ErrorLog ${APACHE_LOG_DIR}/error.log
   CustomLog ${APACHE_LOG_DIR}/access.log combined
</VirtualHost>
```



#### 2.修改/etc/hosts 文件(相当于本地C:\Windows\System32\drivers\etc\hosts)

`127.0.0.1   www.aaa.com
127.0.0.1   www.bbb.com`



#### 3.重启apache，`systemctl restart apache2`



#### 4.完成
