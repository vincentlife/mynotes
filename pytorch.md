# tensor
## 类型转换
* t.type(dtype=None) dtype为None返回tensor类型，不为None执行类型转换

## 创建
```
torch.Tensor(*size,requires_grad=False) 

torch.eye(n, m=None) 
torch.linspace(start, end, steps=100) 
torch.ones(*sizes) 
torch.range(start, end, step=1)
```

## 梯度
### detach作用
假设有模型A和模型B，我们需要将A的输出作为B的输入，但训练时我们只训练模型B. 
input_B = output_A.detach()， 它可以使两个计算图的梯度传递断开

## 运算
### add
```
x + y

torch.add(x, y)

result = torch.empty(5, 3)
torch.add(x, y, out=result)

# in-place的加
y.add_(x)
```
tensor函数名带_后缀的，都是in-place的,如x.copy_(y), x.t_()，是改变tensor的。

### other
* torch.sum(input, dim, keepdim=False, dtype=None)
* torch.var(input, unbiased=True) 
* torch.var(input, dim, keepdim=False, unbiased=True, out=None) 
* torch.min(input, dim, keepdim=False, out=None)

* torch.unique(input, sorted=False, return_inverse=False, dim=None)
sorted 返回结果是否排序
* torch.sort(input, dim=None, descending=False, out=None) 
* torch.topk(input, k, dim=None, largest=True, sorted=True, out=None)


### 逻辑关系
* equal | eq ， eq是逐元素的，equal返回整体是否相等，==等价于eq
* torch.nonzero 返回（z, n）张量，z表示有多少个非0，n = len(shape)，以坐标的形式
* ge gt le lt


### numpy
```
# one element tensor用item来获取值
x = torch.randn(1)
x.item()

a = torch.ones(5)
b = a.numpy()

# b的值也跟着加1。 除了CharTensor，所有在CPU上的tensor都支持和numpy的互转 
a = np.ones(5)
b = torch.from_numpy(a)
np.add(a, 1, out=a)
```

### cuda tensor
```
device = torch.device("cuda")
y = torch.ones_like(x, device=device)  # 直接创建cuda tensor
x = x.to(device) # 或者是to("cuda")
z = x + y # print(z) ---> tensor([2.9218], device='cuda:0')
print(z.to("cpu", torch.double)) # tensor([2.9218], dtype=torch.float64)
```


model.cuda()直接改变。和nn.Module不同，调用tensor.cuda()只是返回这个tensor对象在GPU内存上的拷贝，而不会对自身进行改变。因此必须对tensor进行重新赋值，即tensor=tensor.cuda().


## 操作
### view
```
# 如果该维度值为1，则去掉，否则不变
a.squeeze(dim=None) 
# 增加维度
a.unsqueeze(dim=None)  

# np.concatenate
torch.cat(inputs, dim=0) 
# 沿着一个新维度对输入张量序列进行连接。 序列中所有的张量都应该为相同形状。  
torch.stack(sequence, dim=0)
```

### chunk | split 
* torch.chunk(tensor, chunks, dim=0)

* torch.split(tensor, split_size, dim=0)  将输入张量分割成相等形状的chunks（如果可分）。 如果沿指定维的张量形状大小不能被split_size 整分， 则最后一个分块会小于其它分块


### gather | index_select | masked_select

# 容器
## class torch.nn.Module
```
class Model(nn.Module):
    def __init__(self):
        super(Model, self).__init__()
        self.conv1 = nn.Conv2d(1, 20, 5)# submodule: Conv2d
        self.conv2 = nn.Conv2d(20, 20, 5)
        # 与上句等价，可通过name属性获取
        self.add_module("conv2", nn.Conv2d(10, 20, 4)) 

    def forward(self, x):
       x = F.relu(self.conv1(x))
       return F.relu(self.conv2(x))

m = Model()
m.children() # 获取子模块
m.modules() # 获取所有模块
# 将所有的模型参数赋值CPU|GPU，利用to可以编写不限制设备的代码
m.cpu()
m.cuda()
device = torch.device("cuda" if use_cuda else "cpu")
model = m.to(device)

m.double() # 所有参数类型转换
m.parameters(memo=None) # 返回所有参数，一般用来当作optimizer的参数

# 模型的模式,仅仅当模型中有Dropout和BatchNorm才会有影响。
# 一定注意切换，指定eval时会自动把BN和DropOut固定住，不会取平均，而是用训练好的值，不然的话，一旦test的batch_size过小，很容易就会被BN层导致失真
m.eval()
m.train()
zero_grad() #设置0梯度

# 将state_dict（字典类型）中的parameters和buffers复制到此module和它的后代中
load_state_dict(state_dict)
# 返回state_dict，保存着module的所有状态
state_dict(destination=None, prefix='')
```

## class torch.nn.Sequential(* args)
顺序的容器
```
model = nn.Sequential(nn.Conv2d(1,20,5),nn.ReLU())
# OrderedDict
model = nn.Sequential(OrderedDict([('conv1', nn.Conv2d(1,20,5)),('relu1',nn.ReLU())]))
```