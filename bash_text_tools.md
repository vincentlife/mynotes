# head tail
-q 隐藏文件名
-v 显示文件名
-c<字节> 显示字节数
-n<行数> 显示的行数


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
### 分组

### 引号
* 双引号：awk 'BEGIN{print "\""}' 要print的内容用双引号包围
* 单引号：awk 'BEGIN{print "'\''"}'