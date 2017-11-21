# Install
https://github.com/teddysun/lamp.git

# Apache
centos
* yum install httpd
安装
* systemctl status | enable | start | restart | stop httpd.service
enable 重启服务器自动启动Apache 服务

* vim /etc/httpd/conf/httpd.conf
打开Apache 配置文件

## iptable
systemctl status | enable | start | restart | stop iptables.service 

## firewalld 
systemctl status | enable | start | restart | stop firewalld.service

## httpd.conf



User apache 
Group apache

启动服务后转换的身份，在启动服务时通常以root身份，然后转换身份，这样增加系统安全

# mysql
