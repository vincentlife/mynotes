# DataFrame & Series
## basic
### init 
* DataFrame(np.ndarray,index=,columns=) # index 是行索引 columns是列名
* Series(data=,index=,dtype=,name=) 其中data可以为dictionary Categorical 生成器对象等

### 字符串读入
from io import StringIO
newfile = StringIO(content.decode("utf-8")) # python 2
newfile = StringIO(content) # python 3

### read_csv()
* sep : str, default ‘,’
指定分隔符。如果不指定参数，则会尝试使用逗号分隔。分隔符长于一个字符并且不是‘\s+’,将使用python的语法分析器。并且忽略数据中的逗号。正则表达式例子：'\r\t'
delimiter : str, default None
定界符，备选分隔符（如果指定该参数，则sep参数失效）
 
* header : int or list of ints, default ‘infer’
指定行数用来作为列名，数据开始行数。如果文件中没有列名，则默认为0，否则设置为None。如果明确设定header=0 就会替换掉原来存在列名。header参数可以是一个list例如：[0,1,3]，这个list表示将文件中的这些行作为列标题（意味着每一列有多个标题），介于中间的行将被忽略掉。注意：如果skip_blank_lines=True 那么header参数忽略注释行和空行，所以header=0表示第一行数据而不是文件的第一行。

* index_col : int or sequence or False, default None
用作行索引的列编号或者列名，如果给定一个序列则有多个行索引。
如果文件不规则，行尾有分隔符，则可以设定index_col=False 来是的pandas不适用第一列作为行索引。

* squeeze : boolean, default False
如果文件值包含一列，则返回一个Series

* skiprows : list-like or integer, default None
需要忽略的行数（从文件开始处算起），或需要跳过的行号列表（从0开始）。

### to_csv()
* path_or_buf : string or file handle, default None
File path or object, if None is provided the result is returned as a string.
* sep : character, default ‘,’
Field delimiter for the output file.
* na_rep : string, default ‘’
Missing data representation
* columns : sequence, optional
Columns to write
* header : boolean or list of string, default True
* index : boolean, default True Write row names (index)
* index_label : string or sequence, or False, default None
Column label for index column(s) if desired. If None is given, and header and index are True, then the index names are used. A sequence should be given if the DataFrame uses MultiIndex. If False do not print fields for index names. 
* line_terminator : string, default '\n'
The newline character or character sequence to use in the output file

### df.columns & df.index 
为pandas的索引类型
df.columns[0] 获取列名
df.columns[[0,1,2]] 获取列名,返回索引类型,需要tolist()转换成list 形式 
df.index 同理
se只有index

* df.set_index(keys, drop=True, append=False, inplace=False, verify_integrity=False)
* 


### df.values 
ndarry类型
df.values[:, :] 进行分片
series.values 也是ndarray

### 遍历
+ for colname in df 列名
+ df.iterrows() 
返回一个tuple (index, Series)，这里index 为行索引
+ df.iteritems() 迭代器对象，返回(index, Series)  这里index 为列索引
+ se.iteritems() 返回(index,value)

### 类型转换
* df["A"].astype(numpy.dtype) 将数据转换成numpy.dtype
* df.infer_objects() 如果数据很多无法判断数据类型,推断类型
* pd.to_numeric 把所有的变量都变成了float64

### join
    DataFrame.join(other, on=None, how='left', lsuffix='', rsuffix='', sort=False)[source]
on : column name, array-like column names, 是None则用index
* left: use calling frame’s index (or column if on is specified)
* right: use other frame’s index
* outer: form union of calling frame’s index (or column if on is specified) with * other frame’s index, and sort it lexicographically
* inner: form intersection of calling frame’s index (or column if on is specified) with other frame’s index, preserving the order of the calling’s one

### merge
    DataFrame.merge(right, how='inner', on=None, left_on=None, right_on=None, left_index=False, right_index=False, sort=False, suffixes=('_x', '_y'), copy=True, indicator=False, validate=None)

### pd.concat() 
沿轴拼接 pd.concat([example1, example2], axis=1) 


## 操作
### 增
尽力避免incrementally build a dataframe
* df.append(s, ignore_index=True) 添加行 
* df.add(other=, axis=, fill_value=, level= ) other可以是Series和DataFrame，返回DataFrame
* df["new_column"] = s 添加列 其中列的index需要和df的column一致。 尽量避免这种方式，采用df2.loc[:, 'd'] = d
* df.insert(loc=,column=,value= )
* df.assign(name = Series) 推荐方式，增加新列,返回一个新的DataFrame

### 查
+ df['A'] 获取A列，等价于 df.A 返回Series类型
+ df.loc[:,['A','B']] 按标签查询。格式为行，列。需要注意的是，dataframe的索引[1:3]是包含1,2,3的，与一般python不同。
+ df.iloc[3:5,0:2] 按位置查询，或者df.iloc[[1,2,4],[0,2]]。
+ df.at[rows[0],'A'] 获取标量值，等价于df.loc[rows[0],'A']
+ df.iat[1,1]可获取标量
+ df.ix(1) df.ix('e') 混合索引,先用loc的方式来索引，索引失败就转成iloc的方式

### 删
* df.drop(["column"],axis=1) axis=1是删除列
* df.drop(df.columns[[0,1]],axis=1) 删除0,1 列

### 改
* df.at[dates[0],'A'] = 0 按标签赋值
* df.iat[0,1] = 0 按位置赋值
* df.loc[:,'D'] = np.array([5] * len(df)) 按列赋值
* df2[df2 > 0] = -df2 赋值


### 布尔索引
根据true false系列来索引，demo：
* df[df.A > 0] 
* df2[df2['E'].isin(['two','four'])]
* data.loc[(data["Gender"]=="Female") & (data["Education"]=="Not Graduate") & (data["Loan_Status"]=="Y"), ["Gender","Education","Loan_Status"]]

### apply系列
apply 既可以操作 DataFrame数据，也可以操作Series数据。
apply(func=,axis=)
func接收依据axis确定的series，若func返回series类型则apply返回dataframe类型，若其它类型则apply返回series类型 

applymap 不分行、列，对所有元素进行操作。 
操作对象可以是DataFrame 或者 Series

map 仅面向 Series 类型数据



### 其他
* df.map({}) 传入字典或函数。df['food'].map(str.lower).map({'A':'ab'}})
* df.replace() data.replace([-999, -1000], np.nan)
计算时一般不包括丢失的数据
* df.count() 统计非空
* df.T 转置
* df.sort_index(axis=1, ascending=False) 按轴排序
* df.sort_values(['A','B'],ascending=True) 按值排序
* idxmax() idxmin(axis) 返回最大值/最小值的index
* isin(list-like) 返回True False的series判断是否在list中

### 计算类
* df.mean() 
* df.corr(method='pearson', min_periods=1) min_periods 表示需要的最小observations的数目
* df.diff(periods=1, axis=0) 做一阶差分(连续相邻两项之差) periods 为移动的幅度

### 特征工程相关
* df.describe()
* pd.crosstab(df["column1","column2"])
* df["A"].count() df.count() 统计非空数量
* df.dropna(how='any')
* df.fillna()
* df.isnull() 或者 pd.isnull(df) 返回true false 的dataframe notnull同理 
* df.drop_duplicates(subset=None, keep='first', inplace=False)
subset : column label or sequence of labels, optional
keep : {‘first’, ‘last’, False}, default ‘first’
inplace : boolean, default False

### cut
pd.cut(x, bins, right=True, labels=None, retbins=False, precision=3, include_lowest=False) 
* bins： int 或者是 
bins = [18, 25, 35, 60, 100] cats = pd.cut(ages, bins)
返回一个特殊的Categorical对象，levels为分类名称，labels为结果。


### qcut
* pd.qcut(df['Column'], 4) 根据样本分位数对数据进行bin划分,大小基本相等
* pd.get_dummies(data, prefix=None, prefix_sep='_', dummy_na=False, columns=None, sparse=False, drop_first=False)
 data array-like, Series, or DataFrame
return DataFrame or SparseDataFrame

### 分组 
#### groupby
df.groupby(by=,as_index=)
* by = ["A"] 或 ["A","B"]传入多个结果会显示多个
* as_index True or False 传入的列是否作为索引显示
返回 groupby Object，此时未进行任何计算，groupby Object有以下方法:
* mean() 分组平均值 返回dataFrame
* size() 每组个数
* get_group()
* agg(func) 对分组后的数据应用func函数,agg函数内调用的函数只能对分组进行聚合使用
* apply(func) func(df)接收一个DataFrame对象，该对象包含组内的数据

#### pivot_table


### plot
plot(kind="",) 或直接plot.hist
kind : str
    ‘line’ : line plot (default)#折线图
    ‘bar’ : vertical bar plot#条形图
    ‘barh’ : horizontal bar plot#横向条形图
    ‘hist’ : histogram#柱状图
    ‘box’ : boxplot#箱线图
    ‘kde’ : Kernel Density Estimation plot#Kernel   的密度估计图，主要对柱状图添加Kernel 概率密度线
    ‘density’ : same as ‘kde’
    ‘pie’ : pie plot#饼图
    ‘scatter’ : scatter plot#散点图

plot参数:
figsize: tuple (10,10)



## Series操作
### 方法
* value_counts() 统计各类的数目


### str
提供字符串处理方法，NA值依然为NA
* s.str.split("_")
* s.str.lower()
* s.str.extract(' ([A-Za-z]+)\.', expand=False) 根据正则来提取字符串expand=True返回DataFrame
* s.str.contains
* s.str.get()
* s.str.pad() 左右补齐 

# Categorical


