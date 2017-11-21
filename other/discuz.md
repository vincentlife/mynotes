# install
## lamp环境

## upload
将upload文件夹上传
并 chmod 777(755)


## 修改httpd.conf
DocumentRoot"/var/www/html"

<IfModule dir_module>
    DirectoryIndex index.php
</IfModule>

LoadModule php7_module modules/libphp7.so
AddType application/x-httpd-php .php
DirectoryIndex index.php index.htm index.html