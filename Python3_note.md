# encoding
* ord(c) 返回一个Unicode字符的int类型的序号
* chr(i) 与ord相反，返回Unicode字符

# pythonic code
## 解包，传参
```
# 高级解包 
a, b, *rest = range(10) 
a, *rest, b = range(10)
# 传参 * args 为列表参数 ** kwargs 为字典参数
func(*[1],{'a':1,'b':2})  
```

## slice
* 反向输出字符串 'test'[::-1]
* l[1:9:-1] 取区间[1, 9)，取步长为-1的时候返回空集
* l[9:1:-1] 取区间[9, 1), 取步长为-1的时候返回9到2
...可以用来代替所有的冒号，比如a[:,:,:,1]可以用a[..., 1]来代替

## sort
* sort(cmp=None, key=None, reverse=False cmp和key均为函数 reverse = True 降序
* min/max 取字典最值键：min(dict.items(), key=lambda x: x[1])[0]

## collections
* set的写法 set([]) ->  {} 称为set literal
* 使用dictionary实现switch dict = {key:arg} ,arg可以是function, dict.get(key,default)
* 两个列表生成字典 
    * dict(map(lambda x,y:[x,y],list1,list2))
    * dict(zip(list1,list2))
    * {k:v for k,v in zip(l1,l2)}


## with
* 打开多个文件
with open('file1') as f1, open('file2') as f2, open('file3') as f3: 或者
with nested(open('file1'), open('file2'), open('file3')) as (f1,f2,f3):


# knowledge
## property
@property 用法： 控制访问权限
```
class A:
    def __init__(self, name):
        self._name = name

    @property
    def name(self):
        return self._name

    @name.setter
    def name(self, value):
        self._name = value
```

**property函数** 是@property的令一种写法
```
class A
    def __init__(self, name):
        self._name = name

    def get_name(self):
        return self._name

    def set_name(self, value):
        self._name = value

    name = property(fget=get_name, fset=set_name, fdel=None, doc='name of an animal')
```


## 数值
* // 取整除。 int 用/ 得到浮点数
* float("inf"), float("-inf") 正负无穷。当涉及 > 和 < 运算时，
所有数都比-inf大，所有数都比+inf小。+inf 和 +inf相等，-inf 和 -inf相等。利用 inf 乘以0会得到 not-a-number(NaN)。除了inf外的其他数除以inf，会得到0。

* for else语句 在for循环完整完成后才执行else；如果中途从break跳出，则连else一起跳出。
* enumerate() for index，text in enumerate(list):
* sys.argv[0] 脚本名 sys.argv[1] 第一个参数
* isinstance(obj,type)
* 保留小数 方法一： print(round(a/b,2)) 方法二：print(format(b,'.2f'))
* 最大的int型 python3中为sys.maxsize (python2中为maxint) 最大的浮点数 float(‘inf’)

* python 传参 如果传的参数类型是不可改变的，如基本类型，String类型、元组类型，函数内如需改变参数的值，则相当于重新新建了一个对象。
* 下列对象的布尔值都是False：
1. NONE 或 False(布尔类型)
2. 所有的值为零的数 包括整型 浮点型等等
3. ""(空字符串) [](空列表) ()(空元组) {}(空字典)

## 判断系统
```
import platform
sysstr = platform.system()
if sysstr == "Windows":
    pass
```

# 列表推导
* 列表推导式 [i*2 for i in range(10) if i > 3] PS:python2中xrange被range取代
* x1 if c1 else x2 if c2 else x3 列表推导中的if else 嵌套
* 生成字典 {k:v for k,v in zip(l1,l2)}

# copy
copy.copy() copy.deepcopy() 深拷贝和浅拷贝


# import
可以被import语句导入的对象是以下类型：

* 模块文件（.py文件）
* C或C++扩展（已编译为共享库或DLL文件）
* 包（包含多个模块）
* 内建模块（使用C编写并已链接到Python解释器中）

import使一个变量名引用整个模块对象，因此必须通过模块名称来得到该模块的属性（例如，module1.printer）。而from会把变量名复制到另一个作用域，所以它就可以直接在脚本中使用复制后的变量名，而不用通过模块。 

两种运行python的模式
python xxx.py  直接运行
python -m xxx.py 把模块当作脚本来启动

直接启动是把run.py文件，所在的目录放到了sys.path属性中。
模块启动是把你输入命令的目录（也就是当前路径），放到了sys.path属性中

# attr
## getattr
* getattr(Instance , 'name, 'not find') #如果Instance 对象中有属性name则打印self.name的值，否则打印'not find'
* print getattr(a, 'method', 'default')   
如果有方法method，否则打印其地址，否则打印default   
* print getattr(a, 'method', 'default')()   
如果有方法method，运行函数并打印None否则打印default


# iterator constructor
生成器只能遍历一次
* 生成器函数
以yield代替return
* 生成器表达式
将列表推导的中括号，替换成圆括号，就是一个生成器表达式：(x**2 for x in range(5))

## itertools
### islice

### product
笛卡尔积 
单个 itertools.product(lista, repeat = 2)
两个 itertools.product(a,b)
返回 itertools.product 迭代器对象

### 排列 permutations
itertools.permutations(iterableA, r)
### 组合 combinations
itertools.combinations(iterableA, r)
itertools.combinations_with_replacement(iterable, r) 组合包含自身重复

# lambda
lambda x:x+1
if else 必须都有
( lambda x, y: x if x < y else y )( 1, 2 ) 
科里化
( lambda x: ( lambda y: ( lambda z: x + y + z  )( 1 ) )( 2 ) )( 3 ) 
递归 
func = lambda n: 1 if n == 0 else n * func( n - 1 )


## map filter reduce
如果可以使用列表推导就不要用这三个方法
* map(func,iterable)
* filter(func,iterable)
python 3 filter() 返回filter对象 需要list(filter)
* reduce(lambda x, y: x + y, foo)
python3 需要 from functools import reduce 


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

## collections.OrderedDict
使用OrderedDict会根据放入元素的先后顺序进行排序
OrderedDict() 或OrderedDict.fromkeys(listlike,value) 根据listlike来创建列表 **注意**value没有经过copy，若是list会出问题。
除普通字典外的方法:
popitem(按照后进先出原则，删除最后加入的元素，返回key-value)
pop(获取指定key的value，并在字典中删除)
move_to_end(指定一个key，把对应的key-value移到最后)
setdefault(获取指定key的value，如果key不存在，则创建)

# io
## io.StringIO
StringIO经常被用来作为字符串的缓存，应为StringIO有个好处，他的有些接口和文件操作是一致的，也就是说用同样的代码，可以同时当成文件操作或者StringIO操作。
s = StringIO() 或 s = StringIO("hello world")

StringIO类中的方法： 
read readline readlines write writeline 
getvalue 此函数没有参数，返回对象s中的所有数据
truncate 从读写位置起切断数据，参数size限定裁剪长度，缺省值为None。
tell 返回当前读写位置
seek seek(0) 注意在写入StringIO后指针移动了，需要将指针再seek到开头。
close flush 

