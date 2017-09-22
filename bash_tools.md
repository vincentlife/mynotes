# kill
kill %任务号
kill pid

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

来自: http://man.linuxde.net/sort

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