# ndarray
ndarray默认不使用矩阵运算，如果希望对数组进行矩阵运算的话需要调用相应的函数。而matrix默认使用矩阵运算。为了避免混淆,一般全部采用ndarray

## 创建数组：
* arange()创建一维数组；
* array() 创建一维或多维数组，其参数是类似于数组的对象，如列表等
* ones(shape)：全1 
* zeros(shape)：全0 
* eye(M=3,N=2,k=1) 对角矩阵，从中间第k条对角线为1 其余为0，N表示返回前N行
* identity(n) 单位阵
* empty(shape)：返回无初始化的矩阵（每个数接近0）
* diag(v,k) v是向量,从中间第k条对角线起生成对角阵
* linspace 如np.linspace(1,6,10)则得到1到6之间的均匀分布，总共返回10个数

## 属性
* a.flat 这是一个遍历整个数组的迭代器 for element in b.flat: ，让a中数组元素都被1覆盖 a.flat=1
* a.shape 数组每一维度的大小 a.ndim 数组维度
* a.nbytes==a.size*a.itemsize size: a中所有元素的个数 itemsize 单个元素的字节数,取决于dtype
* a[np.newaxis] 增加维度 np.expand_dims() 增加维度
* a.T 转置数组
* 读取数组元素 a[0],a[0,0] 或者 a.item((2,2)) 取2,2处的值 
* 修改数组中的值 a.itemset((2,2),0) 将2,2处赋值为0 
* s[i:j:k]是从i到j与第k步。a[::3]就是全部的每3份
* a[...,1] 用...省略了所有冒号
* 布尔运算 如arr[(arr>3) & (arr < 100)] **注意括号**

## 方法
* ndarray.flatten() 将多维数组降位一维,返回的是copy，不影响原矩阵
* a.fill(b) 将a中元素都置为b
* a.astype(np.float32) 转换类型
* a.tolist() tofile() tostring() tobytes()


## np方法
### 判断
* np.isnan()
* np.isreal(a) 

* np.argwhere() 返回下标
* np.where() 返回满足条件的数组元素的索引值，比如arr < 1
* np.extract([条件],a) 返回满足条件的数组
* np.take(inds, axis=) 比如a.take([0,3],axis=1) 从axis=1提取0,3 

* np.put()
* np.insert(arr,obj,value,axis=None) obj:为目标位置 value为插入的数值 
* np.append(arr,values,axis=None)
* np.delete(arr,obj,axis=None) obj 目标位置, int型或int型组成的向量

* np.stack([a1,a2,a3],axis=) 将list中的ndarray
* np.concatenate[a1,a2,a3],axis=)
* np.split(ary, indices_or_sections, axis=0)
* reshape & resize reshape 得到copy resize 直接改变数组的形状. reshape中的一个维度可以为-1，这个维度将被推断出。
* ravel() 将多维数组降位一维,返回的是viewer，影响原矩阵, flatten返回的是copy 不影响原矩阵
* np.squeeze() 移除长度为1的轴


* np.apply_along_axis(func1d, axis, arr, *args, **kwargs) axis为int型，在一个维度上
* np.apply_over_axes(func, a, axes) axes为array_like, 在多个维度上
* np.sort(a,axis=) array.sort()是就地排序,改变数组.默认升序,要实现降序排序可以-sort(-array) 
* np.argsort(a) 排序后返回下标

* np.sign(a)，返回数组中各元素的正负符号，用1和-1表示
* np.rint(a) 对浮点数取整，但不改变浮点数类型
* np.piecewise(a,[条件]，[返回值]) 可以分段给定取值, 如np.piecewise(c, [c>0, c<0], [-1,1])
* np.clip(a,a_min,a_max) 将数组中小于a_min的数均换为a_min，大于a_max的数均换为a_max
* np.pad(array, pad_width, mode) pad_width填充的形状, 有多少个维度就有多少个tuple(left,right)
  mode: constant 常数 0 edge 边缘的 mean maximum minimum median 


# 计算
* np.mod(a,n)相当于a%n，np.fmod(a,n)仍为求余且余数的正负由a决定
* np.average(a,b),计算加权平均值 其中b是权重
* np.ptp(a,axis)  (maximum - minimum) along an axis.
* sqrt square absolute log log10 exp
* min,max,sum,mean,std,var,  同时可以使用axis指定对哪一维进行操作, 那个维就消失，其他维不变 , axis为none时计算所有值
* prod(axis) 所有元素乘积
* cumsum和cumprod 返回由中间结果组成的数组
* np.array_equal(a,b) 逐元素比较
* np.maximum(a,b,c,…..)  minimum 多个数组的对应位置上元素大小的比较：返回每个索引位置上的最大值
* np.round()
* np.around()

# 逻辑运算
## logical
logical_and logical_or

## bitwise
bitwise_and bitwise_or bitwise_xor
& | 等价于 bitwise

只支持 integer 和 boolean，对整型是按位操作

## 矩阵相关
* np.dot(a,b)，即得到a*b（一维上是对应元素相乘，多维可将a*b视为矩阵乘法。注意：使用*符号仍然是按位置一对一相乘
* np.trace() 计算矩阵的迹（对角线元素和)
* np.transpose(a,axis=) 返回转置矩阵


## 统计类方法
* numpy.corrcoef(x,y,)
  计算person相关性系数，x可以是1-D 或 2-D ,y 可选填，rowvar为true表示每一行代表一个变量，一般计算特征相关性时rowvar =False,返回相关性矩阵
* np.cov(x)，np.cov(x,y) 计算协方差矩阵


# np.random
* shuffle

## 分布
### binomial
产生二项分布的随机数：np.random.binomial(n,p,size=…)，其中n,p,size分别是每轮试验次数、概率、轮数
### hypergeometric
产生超几何分布随机数：np.random.hypergeometric(n1,n2,n,size=…)，其中参数意义分别是物件1总量、物件2总量、每次采样数、试验次数
### normal
产生N个正态分布的随机数：np.random.normal(均值，标准差，N)
产生N个对数正态分布的随机数：np.random.lognormal(mean,sigma,N)
 multivariate_normal
### multivariate_normal
* mean : 1-D array_like, of length N
* cov : 2-D array_like, of shape (N, N) 协方差矩阵,对称和正定的
* size : int or tuple of ints, optional

## 抽样
### rand
rand(d1,d2,d3,...) 生成指定shape的0,1范围内的随机数
### choice
numpy.random.choice(array, size=None, replace=True, p=None)
从一个int数字或1维array里随机选取内容，如果是int则视作np.arange(n)，并将选取结果放入维度为size的array中返回，当replace为False时，生成的随机数不能有重复的数值，p为array中的元素指定概率。

## 随机状态
* numpy.random.seed()
* get_state() set_state()

# other method
* np.hypot(x1,x2)  求直角三角形的斜边 hypotenuse ，可以用来求平方和
* np.count_nonzero(array,axis) 统计非零项数目,False视为0
* np.bincount()

# 线性代数 np.linalg 
* 最小二乘法估计线性模型中的系数：a=np.linalg.lstsq(x,b),有b=a*x
* 求方阵的逆矩阵：np.linalg.inv(A)
* 求广义逆矩阵：np.linalg.pinv(A)
* 求矩阵的行列式：np.linalg.det(A)
* 解形如AX=b的线性方程组：np.linalg.solve(A,b)
* 求矩阵的特征值：np.linalg.eigvals（A）
* 求特征值和特征向量：np.linalg.eig(A)
*　Svd分解：np.linalg.svd(A)


# 多项式 
* np.poly1d(array) 一元多项式 p = np.poly1d([1,2,3]) 表示1*x^2+2*x+3，p(0.5)计算x=0.5时候的值
* np.polyfit(x,a,n), 拟合点集a得到n级多项式，其中x为横轴长度，返回多项式的系数list
* np.polyder(poly)  传进系数则返回导函数的系数,传入多项式对象则返回导函数的多项式
* 得到多项式的n阶导函数：多项式.deriv(m = n)
* 多项式求根：np.roots(poly)
* 多项式在某点上的值：np.polyval(poly,x[n]),返回poly多项式在横轴点上x[n]上的值
* 两个多项式做差运算： np.polysub(a,b)

# numpy优化
a *= 2 原地操作
a = a*2 隐式拷贝
在python3中都是拷贝
