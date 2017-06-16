# tensor
* device:表示tensor将被产生的设备名称 
* dtype：tensor元素类型 
* graph：这个tensor被哪个图所有 
* name:这个tensor的名称 
* op：产生这个tensor作为输出的操作（Operation） 
* shape：tensor的形状（返回的是tf.TensorShape这个表示tensor形状的类） 
* value_index:表示这个tensor在其操作结果中的索引

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
* tensor.eval(session = sess)
获取张量的值

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

### tf.slice

### tf.split
split(value, num_or_size_splits, axis=0, num=None, name="split")
沿着split_dim维度将value切成num_split块。要求，num_split必须被value.shape[split_dim]整除，即value.shape[split_dim] % num_split == 0。
input = tf.random_normal([5,30])
split0, split1, split2, split3, split4 = tf.split(input,5,0)

### tf.tile
tf.tile(input, multiples, name = None)
通过给定的tensor去构造一个新的tensor。所使用的方法是将input复制multiples次，输出的tensor的第i维有input.dims(i) * multiples[i]个元素，input中的元素被复制multiples[i]次。比如，input = [a b c d], multiples = [2]，那么tile(input, multiples) = [a b c d a b c d]。

### tf.concat()
tf.concat(values, axis, name="concat")
沿着concat_dim维度，去重新串联value，组成一个新的tensor。从直观上来看，我们取的concat_dim的那一维的元素个数肯定会增加。

### tf.reshape()
tf.reshape(tensor, shape, name = None)
对tensor的维度进行重新组合。给定一个tensor，这个函数会返回数据维度是shape的一个新的tensor，但是tensor里面的元素不变。
如果shape是一个特殊值[-1]，那么tensor将会变成一个扁平的一维tensor。
tf.reshape(n,[-1,len(n)]) 结果为 [[...]]

### tf.unstack() tf.stack()
unstack(value,num=None,axis=0,name='unstack')
当axis=0 , shape (A, B, C, D) 变成A个(B,C,D)的tensor
stack(values,axis=0,name='stack') 
tf.stack([x, y, z]) = np.asarray([x, y, z])

### tf.matmul()
矩阵乘法 y = tf.matmul(W, x_data) + b

# seq2seq
## tf.contrib.sequence_loss
sequence_loss(logits, targets, weights,
                  average_across_timesteps=True, average_across_batch=True,
                  softmax_loss_function=None, name=None)
### logits: 
shape [batch_size, sequence_length, num_decoder_symbols], 
* batch_size 指batch大小
* sequence_length 序列长度，指num_steps
* num_decoder_symbols 指输出词库的大小vocab_size
### targets | weights
shape [batch_size, sequence_length]
### 
sequence_loss_by_example的做法是，针对logits中的每一个num_step,即[batch_size, vocab_size], 对所有vocab_size个预测结果，得出预测值最大的那个类别，与target中的值相比较计算Loss值

# tensor board
## Visualizing Learning

## Embedding Visualizing
