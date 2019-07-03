# 图片预处理
ImageDataGenerator

## flow_from_directory
flow_from_directory(self, directory,
                            target_size=(256, 256), color_mode='rgb',
                            classes=None, class_mode='categorical',
                            batch_size=32, shuffle=True, seed=None,
                            save_to_dir=None,
                            save_prefix='',
                            save_format='jpeg',
                            follow_links=False)
directory: 根目录，一个类别一个子目录，子目录下所有格式的图片都会使用
target_size：可是实现对图片的尺寸转换
save_to_dir save_prefix: 可以对处理后图片设置前缀、路径


# aplication
## fine tuning
keras利用预训练权重进行调整,keras的已训练模型是H5PY格式的。h5py.File类似Python的词典对象，可以查看所有的键值
dim_ordering，一张224*224的彩色图片，theano的维度顺序是(3，224，224)，即通道维在前。而tf的维度顺序是(224，224，3)，即通道维在后。 
notop模型
是否包含最后的3个全连接层（whether to include the 3 fully-connected layers at the top of the network）。用来做fine-tuning专用，专门开源了这类模型。 

# 自定义loss和metric
注意编写的函数会被编译成c代码，所以在自定义损失函数中使用eval或session等会出问题

* 报错：range( 1, None) ->typeError : 'NoneType' object cannot be interpreted as an integer  
自定义loss， keras会对score_array求mean，需要loss函数返回的dim需要是确定的，所以 可以再改成tf.reshape(loss, (-1,))