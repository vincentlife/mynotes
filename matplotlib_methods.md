# General
引入包import matplotlib.pyplot as plt，

子图：plt.subplot(abc)，其中abc分别表示子图行数、列数、序号

创建绘图组件的顶层容器：fig = plt.figure()
添加子图：ax = fig.add_subplot(abc)

plt.show()显示图像
## 坐标轴相关
以下均有get set方法
plt.title(‘…’)
plt.xlabel(‘x’), plt.ylabel(‘y’)
plt.xticks(x,x_groups) plt.yticks(y, y_group) 设置刻度对应的点的名称
plt.grid(True) 添加网格线 


## annotation
添加注释：如ax.annotate('x', xy=xpoint, textcoords='offsetpoints',xytext=(-50, 30), arrowprops=dict(arrowstyle="->"))
增加图例：如plt.legend(loc='best', fancybox=True)

## tools
对坐标取对数：横坐标plt.semilogx()，纵坐标plt.semilogy()，横纵同时plt.log

# Gallery
## basic
plt.plot([x1,y1],[x2,y2],"r-") 两点间画线
## meshgrid
delta = 0.2
x = np.arange(-3, 3, delta)
y = np.arange(-3, 3, delta)
X, Y = np.meshgrid(x, y)

## scatter
绘制散点图：plt.scatter(x,y,c = ‘..’,s = ..)，c表示颜色，s表示大小，marker表示形状
* b: blue g: green r: red c: cyan m: magenta y: yellow k: black w: white
* ('o', 'v', '^', '<', '>', '8', 's', 'p', '*', 'h', 'H', 'D', 'd', 'P', 'X')
## hist
绘制方图：plt.hist(a,b)，a为长方形的左横坐标值，b为柱高。alpha是频率分布图的透明度, bins指定bin(箱子)的个数,也就是总共有几条条状图
## contour
X, Y = np.meshgrid(x, y)
plt.contour(X, Y, Z1, linewidths=0.5)

## 3d 
from mpl_toolkits.mplot3d import Axes3D


# Seaborn Methods
## 