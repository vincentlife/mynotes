# scipy结构
scipy几乎实现numpy的所有函数，一般而言，如果scipy和numpy都有这个函数的话，应该用scipy中的版本，因为scipy中的版本往往做了改进，效率更高。但是，有一些同名函数，却有着不同的行为,比如log10，linalg.solve
scipy由一些几乎独立的子模块组成,常用的有
scipy.special 特殊函数 scipy.io 数据输入输出 scipy.linalg 线性代数程序 scipy.stats  统计 scipy.integrate  积分程序 scipy.interpolate  插值

# scipy.special
* expit sigmoid激活函数expit(x) = 1/(1+exp(-x))
* logit  logit(p) = log(p/(1-p)). logit(0) = -inf, logit(1) = inf, and logit(p) for p<0 or p>1 yields nan.

# scipy.sparse
* bsr_matrix(arg1[, shape, dtype, copy, blocksize]) Block Sparse Row matrix
coo_matrix是三元组，不能按行也不能按列切片
* coo_matrix(arg1[, shape, dtype, copy]) A sparse matrix in COOrdinate format.
* csc_matrix(arg1[, shape, dtype, copy]) Compressed Sparse Column matrix
to_csc 是按列压缩的稀疏矩阵，按列切片比较快，可以按行切片

* csr_matrix(arg1[, shape, dtype, copy]) Compressed Sparse Row matrix
to_csr  是按行压缩的稀疏矩阵，按行切片比较快，可以按列切片

* dia_matrix(arg1[, shape, dtype, copy]) Sparse matrix with DIAgonal storage
* dok_matrix(arg1[, shape, dtype, copy]) Dictionary Of Keys based sparse matrix.
* lil_matrix(arg1[, shape, dtype, copy]) Row-based linked list sparse matrix

## 操作
* A = coo_matrix(array)
* A.toarray()
* 可以用hstack,vstack合并相同数据类型的两个稀疏矩阵
* （似乎)除了coo之外稀疏矩阵的存储格式，都可以进行slice操作 
* sparce矩阵的读取。可以像常规矩阵一样通过下标读取。也可以通过getrow(i)，gecol(i)读取特定的列或者特定的行，以及nonzero()读取非零元素的位置。


# scipy.stats
scipy.stats模块主要围绕随机变量提供数值方法，比如随机变量的分位数/cdf之类的，构造分布，分布对象模型之类的。还有一些检验方法，ks检验，t检验，正态性检验，卡方检验之类的.
statsmodels主要围绕着回归模型提供操作方法，如数据访问方式，拟合，绘图，报告诊断等。

## 随机变量
连续随机变量的主要公共方法如下：
rvs:随机变量（就是从这个分布中抽一些样本）
pdf：概率密度函数。
cdf：累计分布函数
sf：残存函数（1-CDF）
ppf：分位点函数（CDF的逆）
isf：逆残存函数（sf的逆）
stats:返回均值，方差，（费舍尔）偏态，（费舍尔）峰度。
moment:分布的非中心矩。



## 检验
### ks检验
卡方检验
chisquare(f_obs, f_exp=None, ddof=0, axis=0)
ks检验
svalue,pvalue =  stats.kstest(x,'norm')
检验 x是否服从正态分布
svalue,pvalue = ks_2samp(data1, data2)
假设data1和data2来自同一分布，为H0。若p值大于0.05，则无法拒绝假设



## 其它
### 相关系数
spearmanr()
