# ftp
ftp domain.com
ftp 192.168.0.1
ftp user@ftpdomain.com 

put get delete dir ls
mput等对多个文件操作

# pure-ftpd
修改配置文件 pure-ftpd.conf
ClientCharset=gbk #必设，防止Windows登录出现中文乱码
DontResolve=yes #不解析域名，可以节省登录时间
BrokenClientsCompatibility=yes #兼容IE等非标准FTP client
ChrootEveryone=yes #把所有用户限制在其homedir下
KeepAllFiles=yes #禁止用户删除文件，TrustedGID组中的除外
TrustedGID=1001 #管理员组ftpadmins的GID，允许管理员删除文件
CreateHomeDir=yes #当虚拟用户第一次登录时，自动创建homedir
MaxClientsPerIP=2 #每个IP限制2个连接
MaxClientsNumber=20 #最大并发连接数，默认值是50
MaxDiskUsage=90 #分区已使用空间超过90%时不再接受上传
NoAnonymous=no #允许匿名登录
Bind=,8821 #改变端口号

## 系统用户策略
sudo groupadd ftpadmins
sudo groupadd ftpusers
sudo useradd -g ftpadmins -d /dev/null -s /bin/false ftpadmin
sudo useradd -g ftpadmins -d /dev/null -s /bin/false ftpuser
sudo useradd -g ftpusers -d /ftp/public -s /bin/false ftpcl
sudo mkdir /ftp
sudo mkdir /ftp/users/

## ftp用户策略 

sudo chown -R ftpadmin:ftpadmins /ftp
sudo chmod -R 755 /ftp
sudo chmod 775 /ftp/users

sudo pure-pw useradd admin -u ftpadmin -d /ftp
pure-pw useradd testuser -u ftpadmin -d /ftp/users/testuser
sudo pure-pw useradd test1 -u ftpuser -d /ftp/users/test1

/www/server/pure-ftpd/bin/pure-pw mkdb
cd /etc/pure-ftpd/auth
sudo ln -s ../conf/PureDB 60puredb

### 目前策略
系统用户
ftpadmin
ftpuser1

需要手动chown ‐R ftpadmin users
chgrp ‐R ftpadmins users




# apache
配置文件一般位置 /etc/httpd/conf/httpd.conf
