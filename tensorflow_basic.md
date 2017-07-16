# tensor
* device:表示tensor将被产生的设备名称 
* dtype：tensor元素类型 
* graph：这个tensor被哪个图所有 
* name:这个tensor的名称 
* op：产生这个tensor作为输出的操作（Operation） 
* shape：tensor的形状（返回的是tf.TensorShape这个表示tensor形状的类） 
* value_index:表示这个tensor在其操作结果中的索引

## tensor.eval(session = sess)
获取张量的值
## tensor.get_shape()
获取维度，是一个Dimension类型的对象，可以用input.get_shape().as_list()[-1]来转换成list

## start
为了便于在 IPython 等交互环境使用 TensorFlow，需要用 InteractiveSession 代替 Session 类,sess = tf.InteractiveSession()
使用 Tensor.eval() 和 Operation.run() 方法代替 Session.run()。

sess.run([tensor1,tensor2]) 取回tensor值
sess.run() 执行操作,如assign.MatMul等

init = tf.global_variables_initializer()，是预先对变量初始化，
Tensorflow 的变量必须先初始化，然后才有值。而常值张量是不需要的。

## IO
* tf.constant()
声明一个常量 ，比如matrix1 = tf.constant([[3., 3.]])
matrix2 = tf.constant([[2.],[2.]])
* tf.Variable()
声明一个变量,同常量
* tf.placeholder()
设计placeholder节点的唯一的意图就是为了提供数据供给(feeding)的方法。placeholder节点被声明的时候是未初始化的， 也不包含数据。

### tf.get_variable
get_variable(name, shape=None, dtype=dtypes.float32, initializer=None,
                 regularizer=None, trainable=True, collections=None,
                 caching_device=None, partitioner=None, validate_shape=True,
                 custom_getter=None):

* name如果在该命名域中之前已经有名字=name的变量，则调用那个变量；如果没有，则根据输入的参数重新创建一个名字为name的变量
* shape: 变量的形状，[]表示一个数，[3]表示长为3的向量，[2,3]表示矩阵或者张量(tensor) 
* dtype: 变量的数据格式，主要有tf.int32, tf.float32, tf.float64等等 
* initializer: 初始化工具，有tf.zero_initializer, tf.ones_initializer, tf.constant_initializer, tf.random_uniform_initializer, tf.random_normal_initializer, tf.truncated_normal_initializer等

## 常用
### tf.ones | tf.zeros
    tf.ones(shape,type=tf.float32,name=None) 
    tf.zeros([2, 3], int32) 

### tf.ones_like | tf.zeros_like
    tf.ones_like(tensor,dype=None,name=None) 
    tf.zeros_like(tensor,dype=None,name=None) 
新建一个与给定的tensor类型大小一致的tensor，其所有元素为1或0

### tf.one_hot
    one_hot(indices,depth,on_value=None,off_value=None,
    axis=None,dtype=None,name=None)
* indices: A Tensor of indices.
* depth: A scalar defining the depth of the one hot dimension.
* axis: The axis to fill (default: -1, a new inner-most axis).
* dtype: The data type of the output tensor.
sample:
indices = [[0, 2], [1, -1]]depth = 3 on_value = 1.0 off_value = 0.0 axis = -1
output shape(2,2,3)

### tf.lin_space | tf.range()
* lin_space(start,stop,num,name=None) a tensor of stop - start / num - 1
数据类型是float32, float64，范围[start,stop]
* range(start, limit, delta=1, dtype=None, name='range')  范围[start,limit)

### tf.random_normal | tf.truncated_normal | tf.random_uniform
* tf.random_uniform([1,2],-1.0,1.0)
随机均匀分布
* tf.random_normal() 随机正态分布
x = tf.random_normal(shape=[1,5],mean=0.0,stddev=1.0,dtype=tf.float32,seed=None,name=None)
* tf.truncated_normal(shape, mean=0.0, stddev=1.0, dtype=tf.float32, seed=None, name=None)
The generated values follow a normal distribution with specified mean and standard deviation, except that values whose magnitude is more than 2 standard deviations from the mean are dropped and re-picked.

## 变换
### tf.expand_dims 
    tf.expand_dims(input, dim, name = None)
图片数据维度是[height, width, channels]，加入“批量”这个信息expand_dims(images, 0)，那么该图片的维度就变成了[1, height, width, channels]dim的值也可以是负数，从尾部开始插入。
’t’ is a tensor of shape [2] 
shape(expand_dims(t, 0)) ==> [1, 2] 
shape(expand_dims(t, 1)) ==> [2, 1] 
shape(expand_dims(t, -1)) ==> [2, 1]

### tf.squeeze
    tf.squeeze(input, squeeze_dims = None, name = None)
将input中维度是1的那一维去掉。但是如果你不想把维度是1的全部去掉，那么你可以使用squeeze_dims参数，来指定需要去掉的位置。

### tf.gather
    tf.gather(params,indices,validate_indices=None,name=None)
从params中取出indces对应的slice，最后输出的数据维度是indices.shape + params.shape[1:]。如tf.gather([ 1 11 21 31],[2,0,1,2]) -> [21,1,11,21]

### tf.slice
    tf.slice(input_,begin,size,name=None)
从begin处抽取size个,begin和size要与input的shape相同

### tf.split
    tf.split(value, num_or_size_splits, axis=0, num=None, name="split")
沿着split_dim维度将value切成num_split块。要求，num_split必须被value.shape[split_dim]整除，即value.shape[split_dim] % num_split == 0。

    input = tf.random_normal([5,30])
    split0, split1, split2, split3, split4 = tf.split(input,5,0)

### tf.tile
    tf.tile(input, multiples, name = None)
通过给定的tensor去构造一个新的tensor。将input复制multiples次，输出的tensor的第i维有input.dims(i) * multiples[i]个元素，input的维度要和multiple的长度一致。input中的元素被复制multiples[i]次。比如，input = [a b c d], multiples = [2]，那么tile(input, multiples) = [a b c d a b c d]。0维有4*2个元素

### tf.concat()
    tf.concat(values, axis, name="concat")
沿着concat_dim维度，去重新串联value，组成一个新的tensor。从直观上来看，我们取的concat_dim的那一维的元素个数肯定会增加。
t1 = [[1, 2, 3], [4, 5, 6]]
t2 = [[7, 8, 9], [10, 11, 12]]
tf.concat([t1, t2], 0) ==> [[1, 2, 3], [4, 5, 6], [7, 8, 9], [10, 11, 12]]
tf.concat([t1, t2], 1) ==> [[1, 2, 3, 7, 8, 9], [4, 5, 6, 10, 11, 12]]

### tf.reshape()
tf.reshape(tensor, shape, name = None)
shape中-1的那一维将由其它维infer出，当tensor是scalar，shape =  [] reshapes to a scalar 

### tf.transpose
    transpose(a,perm=None,name='transpose')
求转置，perm是tensor a的维数的排列(permutation)，比如[2,1,0]，即将3个维度转置

### tf.unstack() tf.stack()
    unstack(value,num=None,axis=0,name='unstack')
当axis=0 , shape (A, B, C, D) 变成A个(B,C,D)的tensor
应用: tf.unstack(tf.shape(tensor)) 获取该tensor每一维大小的scala

stack(values,axis=0,name='stack') 
Given a list of length N of tensors of shape (A, B, C)，if axis == 0 then the output tensor will have the shape (N, A, B, C). if axis == 1 then the output tensor will have the shape (A, N, B, C)

### tf.reduce 系列
* min max mean sum prod 被reduce的维数 (3,2,4) axis=1 -> (3,4),若没有指定维数，则求所有元素
* reduce_all 计算逻辑与(logical and) reduce_any 计算逻辑或(logical or)

### tf.matmul()
    matmul(a, b, 
    transpose_a=False, transpose_b=False, 
    adjoint_a=False,adjoint_b=False, 
    a_is_sparse=False, b_is_sparse=False,name=None)
matmul 只能对2d或3d tensor进行运算
adjoint: conjugated and transposed before multiplication.
3-D  tensor  [2,2,3] * [2,3,2] => [2,2,2]

### tf.multiply
    multiply(x, y, name=None)
每个元素相乘
y: A Tensor. Must have the same type as x
Returns: A Tensor. Has the same type as x

### tf.cond
    cond (pred, true_fn=None, false_fn=None, strict=False, name=None)
sample:

    z = tf.multiply(a, b)
    result = tf.cond(x < y, lambda: tf.add(x, z), lambda: tf.square(y)) 

# distribution
## Multinomial
