# IO
* sys.stdout.write(obj+'\n') print 调用该方法
* 

# encoding
* ord(c) 返回一个Unicode字符的int类型的序号
* chr(i) 与ord相反，返回Unicode字符

# knowledge
* // 取整除。 int 用/ 得到浮点数
* float("inf"), float("-inf") 正负无穷。当涉及 > 和 < 运算时，
所有数都比-inf大，所有数都比+inf小。+inf 和 +inf相等，-inf 和 -inf相等。利用 inf 乘以0会得到 not-a-number(NaN)。除了inf外的其他数除以inf，会得到0。
* 使用zip()可进行两个变量的循环 for i,j in zip(range(2),range(2))
* 交换变量 a,b = b,a
* enumerate() for index，text in enumerate(list):
* 列表推导式 [i*2 for i in range(10)] PS:python2中xrange被range取代
* 使用dictionary实现switch dict = {key:arg} ,arg可以是function, dict.get(key,default) 
* min/max 取字典最值键：min(dict.items(), key=lambda x: x[1])[0]
* l[1:9:-1] 取区间[1, 9)，取步长为-1的时候返回空集
* l[9:1:-1] 取区间[9, 1), 取步长为-1的时候返回9到2


# attr
## getattr
* getattr(Instance , 'name, 'not find') #如果Instance 对象中有属性name则打印self.name的值，否则打印'not find'
* print getattr(a, 'method', 'default')   
如果有方法method，否则打印其地址，否则打印default   
* print getattr(a, 'method', 'default')()   
如果有方法method，运行函数并打印None否则打印default



# iterator constructor
## yield


# lambda
lambda x:x+1


## map
* map(func,iterable)
* 

## filter
* filter(func,iterable)
* python 3 filter() 返回filter对象 需要list(filter)

### reduce
* reduce(lambda x, y: x + y, foo)
* python3 需要 from functools import reduce 

# Decorator
## @property
@property一个getter方法变成属性
@attr.setter，负责把一个setter方法变成属性赋值

# re
* p = re.compile(pattern), p.func(string)
* re.func(pattern,string)

## match
尝试从字符串的起始位置匹配一个模式，如果不是起始位置匹配成功的话，match()就返回none。成功返回Match对象
## search
re.search 扫描整个字符串并返回第一个成功的匹配。成功返回Match对象
## findall
搜索string，以列表形式返回全部能匹配的子串
## sub(pattern, repl, string, count=0, flags=0)
检索和替换
* pattern : 正则中的模式字符串。
* repl : 替换的字符串，也可为一个函数。
* string : 要被查找替换的原始字符串。
* count : 模式匹配后替换的最大次数，默认 0 表示替换所有的匹配。
## split(pattern, string[, maxsplit])
按照能够匹配的子串将string分割后返回列表。maxsplit用于指定最大分割次数，不指定将全部分割。
## finditer(pattern, string[, flags]): 
搜索string，返回一个顺序访问每一个匹配结果（Match对象）的迭代器。 
## Match对象
### 属性
string: 匹配时使用的文本。
re: 匹配时使用的Pattern对象。
pos: 文本中正则表达式开始搜索的索引。值与Pattern.match()和Pattern.seach()方法的同名参数相同。
endpos: 文本中正则表达式结束搜索的索引。值与Pattern.match()和Pattern.seach()方法的同名参数相同。
lastindex: 最后一个被捕获的分组在文本中的索引。如果没有被捕获的分组，将为None。
lastgroup: 最后一个被捕获的分组的别名。如果这个分组没有别名或者没有被捕获的分组，将为None。
### 方法
* group([group1, …]): 
获得一个或多个分组截获的字符串；指定多个参数时将以元组形式返回。group1可以使用编号也可以使用别名；编号0代表整个匹配的子串；不填写参数时，返回group(0)；没有截获字符串的组返回None；截获了多次的组返回最后一次截获的子串。
* groups([default]): 
以元组形式返回全部分组截获的字符串。相当于调用group(1,2,…last)。default表示没有截获字符串的组以这个值替代，默认为None。
* groupdict([default]): 
返回以有别名的组的别名为键、以该组截获的子串为值的字典，没有别名的组不包含在内
* start([group]): 
返回指定的组截获的子串在string中的起始索引（子串第一个字符的索引）。group默认值为0。
* end([group]): 
返回指定的组截获的子串在string中的结束索引（子串最后一个字符的索引+1）。group默认值为0。
* span([group]): 
返回(start(group), end(group))。
* expand(template): 
将匹配到的分组代入template中然后返回。template中可以使用\id或\g<id>、\g<name>引用分组，但不能使用编号0。\id与\g<id>是等价的；但\10将被认为是第10个分组，如果你想表达\1之后是字符'0'，只能使用\g<1>0。

## flag
re.I    使匹配对大小写不敏感
re.L    做本地化识别（locale-aware）匹配
re.M    多行匹配，影响 ^ 和 $
re.S    使 . 匹配包括换行在内的所有字符
re.U    根据Unicode字符集解析字符。这个标志影响 \w, \W, \b, \B.
re.X    该标志通过给予你更灵活的格式以便你将正则表达式写得更易于理解。

## 语法
* re? 匹配0个或1个由前面的正则表达式定义的片段，可以用\*?来进行**非贪婪方式**
* ^   匹配字符串的开头
* $   匹配字符串的末尾。
* .   匹配任意字符，除了换行符，当re.DOTALL标记被指定时，则可以匹配包括换行符的任意字符。 或[.\n]
* \d  匹配一个数字字符。等价于 [0-9]。
* \D  匹配一个非数字字符。等价于 [^0-9]。
* \s  匹配任何空白字符，包括空格、制表符、换页符等等。等价于 [ \f\n\r\t\v]。
* \S  匹配任何非空白字符。等价于 [^ \f\n\r\t\v]。
* \w  匹配包括下划线的任何单词字符。等价于'[A-Za-z0-9_]'。
* \W  匹配任何非单词字符。等价于 '[^A-Za-z0-9_]'。
* [...]   用来表示一组字符,单独列出：[amk] 匹配 'a'，'m'或'k'
* [^...]  不在[]中的字符：[^abc] 匹配除了a,b,c之外的字符。
* re* 匹配0个或多个的表达式。
* re+ 匹配1个或多个的表达式。

# collections
## collections.Counter()
* c.update(key) # key对应计数加一
* c.subtract(key) # key对应计数减一
* sum(c.values())  # 所有计数的总数
* c.clear()  # 重置Counter对象，注意不是删除
* list(c)  # 将c中的键转为列表
* set(c)  # 将c中的键转为set
* dict(c)  # 将c中的键值对转为字典
* c.items()  # 转为(elem, cnt)格式的列表
* Counter(dict(list_of_pairs))  # 从(elem, cnt)格式的列表转换为Counter类对象
* c.most_common()[:-n:-1]  c.most_common(n) # 取出计数最少的n个元素
* c += Counter()  # 移除0和负值
* +、-、&、|操作也可以用于Counter。其中&和|操作分别返回两个Counter对象各元素的最小值和最大值。需要注意的是，得到的Counter对象将删除小于1的元素。

## collections.defaultdict()
* 采用一个类型初始化d = defaultdict(list)当所访问的键不存在的时候，可以实例化一个值作为默认值。初始化：int：0，float: 0.0, str ""
* 自定义默认值 dd = defaultdict(lambda x:0)

# magic methods

