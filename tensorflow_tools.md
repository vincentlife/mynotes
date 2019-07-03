## session
为了便于在 IPython 等交互环境使用 TensorFlow，需要用 InteractiveSession 代替 Session 类,sess = tf.InteractiveSession()
使用 Tensor.eval() 和 Operation.run() 方法代替 Session.run()。

sess.run([tensor1,tensor2]) 取回tensor值
sess.run() 执行操作,如assign.MatMul等

init = tf.global_variables_initializer()，是预先对变量初始化，
Tensorflow 的变量必须先初始化，然后才有值。而常值张量是不需要的。

tensor.eval(session = sess) 传入sess得到tensor的值


# tensor board
## Visualizing Learning

## Embedding Visualizing