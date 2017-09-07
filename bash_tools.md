# pip
* pip install name /name.whl /url
* pip install --upgrade
* pip uninstall
* pip install -r requirements.txt 
* pip install --user
pip install --user follows four rules:

    - When globally installed packages are on the python path, and they conflict with the installation requirements, they are ignored, and not uninstalled.

    - When globally installed packages are on the python path, and they satisfy the installation requirements, pip does nothing, and reports that requirement is satisfied (similar to how global packages can satisfy requirements when installing packages in a --system-site-packages virtualenv).

    - pip will not perform a --user install in a --no-site-packages virtualenv (i.e. the default kind of virtualenv), due to the user site not being on the python path. The installation would be pointless.

    - In a --system-site-packages virtualenv, pip will not install a package that conflicts with a package in the virtualenv site-packages. The --user installation would lack sys.path precedence and be pointless. 

* pip show
* pip search "query"

# juypter
## run 
jupyter notebook 
## 远程访问
1. 生成配置文件
$jupyter notebook --generate-config
2. 生成密码
打开ipython，创建一个密文的密码：
In [1]: from notebook.auth import passwd 
In [2]: passwd()
Enter password:  
Verify password:  
Out[2]: 'sha1:ce23d945972f:34769685a7ccd3d08c84a18c63968a41f1140274' # 生成hash值
这里如果无法打开ipython，可以直接用命令行
root@docker_admin:~# python -c "import IPython;print IPython.lib.passwd()" 
3. 修改config文件
~/.jupyter/jupyter_notebook_config.py
c.NotebookApp.ip='*'
c.NotebookApp.password = u'sha:ce...刚才复制的hash'
c.NotebookApp.open_browser = False 
c.NotebookApp.port =8888 

# kill
kill %任务号
kill pid

# awk
* awk '{print $3 "\t" $4}' marks.txt 打印第三列和第四列，从1开始
* awk '/a/ {print $0}' marks.txt 判断每一行中是否包含a，如果包含则打印该行。$0表示当前行，body 缺失会默认执行打印，所以等价于awk '/a/' marks.txt
* $ awk '/a/ {print $4 "\t" $1}' marks.txt 打印匹配行的3、4列
* awk '/a/{++cnt} END {print "Count = ", cnt}' marks.txt 统计匹配上的行数

## 内置变量
* ARGC               命令行参数个数
* ARGV               命令行参数排列
* ENVIRON            支持队列中系统环境变量的使用
* FILENAME           awk浏览的文件名
* FNR                浏览文件的记录数
* NF                 浏览记录的域的个数
* NR                 已读的记录数
* FS                 设置输入域分隔符，等价于命令行 -F选项
* OFS                输出域分隔符
* ORS                输出记录分隔符(行)
* RS                 控制记录分隔符(行)

## 双向管道
使用|&进行双向连接，发送数据到另一个程序处理，然后读取处理结果。

## demo
### 更改分隔符
'BEGIN {FS="\t";OFS="|"} { print $1, $2, $3}' 修改输入分隔符为','输出分隔符为'|'

### 输出标题行和符合条件的行
'BEGIN { FS="\t" } NR ==1 || ($5 == "Female" && $4 ~ /@facebook\.com$/) { print $0 }'
~ 是正则匹配操作符，/ / 里面是正则表达式。最后一个$在正则表达式中表示行的结尾。
### first 100
NR == 1, NR == 100 { print $0 }
### 引号
* 双引号：awk 'BEGIN{print "\""}' 要print的内容用双引号包围
* 单引号：awk 'BEGIN{print "'\''"}'


# grep
## 参数
* -c 只输出匹配行的计数
* -i 不区分大小写（用于单字符）
* -n 显示匹配的行号
* -v 不显示不包含匹配文本的所以有行
* -s 不显示错误信息
* -E 使用扩展正则表达式

# find 
-cmin<分钟>：查找在指定时间之时被更改过的文件或目录；
-cnewer<参考文件或目录>查找其更改时间较指定文件或目录的更改时间更接近现在的文件或目录； 
-ctime<24小时数>：查找在指定时间之时被更改的文件或目录，单位以24小时计算；
-atime<24小时数>：查找在指定时间曾被存取过的文件或目录，单位以24小时计算；
-user<拥有者名称>：查找符和指定的拥有者名称的文件或目录；

## find . -type 类型参数
f 普通文件 l 符号连接 d 目录 c 字符设备 b 块设备 s 套接字
## -regix
find . -regex ".*\(\.txt\|\.pdf\)$"
-iregix 忽略大小写
## -maxdepth 3
向下最大深度为3
## sample
find /home -iname "*.txt" home下txt文件，忽视大小写
find . -type f -newer file.log 找出比file.log修改时间更长的所有文件
find . -type f -name "*.php" ! -perm 644 找出当前目录下权限不是644的php文件
find . -type f -group sunk 找出当前目录用户组sunk拥有的所有文件


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