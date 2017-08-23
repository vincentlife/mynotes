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

# kill
kill %任务号
kill pid

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
