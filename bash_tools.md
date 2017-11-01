# cp mv rm
cp -R 

# kill
kill %任务号
kill pid

# groups
groups [user]

## chmod
mkdir abc
* chmod 755 abc：赋予abc权限rwxr-xr-x
  
* chmod u=rwx,g=rx,o=rx abc：u=用户权限，g=组权限，o=不同组其他用户权限，注意是逗号而不是空格
* chmod u-x,g+w abc：给abc去除用户执行的权限，增加组写的权限
* chmod a+r abc：给所有用户添加读的权限

## chown chgrp
改变所有者（chown）和用户组（chgrp）命令
* chown xiaoming abc：改变abc的所有者为xiaoming
* chown root ./abc：改变abc这个目录的所有者是root
* chown ‐R root ./abc：改变abc这个目录及其下面所有的文件和目录的所有者是root。
  - R 递归式地改变指定目录及其下的所有子目录和文件的拥有者。
* chgrp root abc：改变abc所属的组为root


# sort
sort(选项)(参数,filename)
-b：忽略每行前面开始出的空格字符； 
-c：检查文件是否已经按照顺序排序； -d：排序时，处理英文字母、数字及空格字符外，忽略其他的字符； -f：排序时，将小写字母视为大写字母； -i：排序时，除了040至176之间的ASCII字符外，忽略其他的字符； -m：将几个排序号的文件进行合并； 
-M：将前面3个字母依照月份的缩写进行排序； 
-n：依照数值的大小排序； 
-o<输出文件>：将排序后的结果存入制定的文件； 
-r：以相反的顺序来排序； 
-t<分隔字符>：指定排序时所用的栏位分隔字符； 
+<起始栏位>-<结束栏位>：以指定的栏位来排序，范围由起始栏位到结束栏位的前一栏位。

## -t
分隔符 -t ' '
## -k
-k 1.2,1.3
FStart.CStart Modifie,FEnd.CEnd Modifier -------Start--------,-------End-------- 
FStart.CStart 选项 , FEnd.CEnd 选项
## 

# 权限
- 10个字符确定不同用户能对文件干什么
- 第一个字符代表文件（-）、目录（d），链接（l）
- 其余字符每3个一组（rwx），读（r）、写（w）、执行（x）
- 第一组rwx：文件所有者的权限是读、写和执行
- 第二组rw-：与文件所有者同一组的用户的权限是读、写但不能执行
- 第三组r--：不与文件所有者同组的其他用户的权限是读不能写和执行
- 0表示没有权限，1表示可执行权限，2表示可写权限，4表示可读权限，然后将其相加组成3位数来表示权限


# grep
## 参数
* -c 只输出匹配行的计数
* -i 不区分大小写（用于单字符）
* -n 显示匹配的行号
* -v 不显示不包含匹配文本的所以有行
* -s 不显示错误信息
* -E 使用扩展正则表达式

# find
## -name 
文件名

## -type 类型参数
f 普通文件 l 符号连接 d 目录 c 字符设备 b 块设备 s 套接字

## -regix
find . -regex ".*\(\.txt\|\.pdf\)$"
-iregix 忽略大小写
## -maxdepth 3
向下最大深度为3
## demo
find /home -iname "*.txt" home下txt文件，忽视大小写
find . -type f -newer file.log 找出比file.log修改时间更长的所有文件
find . -type f -name "*.php" ! -perm 644 找出当前目录下权限不是644的php文件
find . -type f -group sunk 找出当前目录用户组sunk拥有的所有文件

## other
* -cmin<分钟>：查找在指定时间之时被更改过的文件或目录；
* -cnewer<参考文件或目录>* 查找其更改时间较指定文件或目录的更改时间更接近现在的文件或目录； 
* -ctime<24小时数>：查找在指定时间之时被更改的文件或目录，单位以24小时计算；
* -atime<24小时数>：查找在指定时间曾被存取过的文件或目录，单位以24小时计算；
* -user<拥有者名称>：查找符和指定的拥有者名称的文件或目录；

# xargs
通常和find一起使用

# less
less [参数]  文件

b  向后翻一页
d  向后翻半页
h  显示帮助界面
Q  退出less 命令
u  向前滚动半页
y  向前滚动一行
空格键 滚动一行
回车键 滚动一页
[pagedown]： 向下翻动一页
[pageup]：   向上翻动一页

# base64
base64 file
echo "string" | base64
echo -n "c25haWx3YXJyaW9y" | base64 -d
-n 选项没有输出字符串结尾的' '换行字符


# du
du -ah --max-depth=1    
a表示显示目录下所有的文件和文件夹（不含子目录），
h表示以人类能看懂的方式
max-depth表示目录的深度。

# diff patch