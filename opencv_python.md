# flags
UNCHANGED flag=-1时，8位深度，原通道
GRAYSCALE flag=0，8位深度，1通道
COLOR flag=1,   8位深度  ，3通道
ANYDEPTH flag=2，原深度，1通道
ANYCOLOR flag =4 

# basic
## resize
INTER_NEAREST - 最近邻插值
INTER_LINEAR - 线性插值（默认）
INTER_AREA - 区域插值
INTER_CUBIC - 三次样条插值
INTER_LANCZOS4 - Lanczos插值
双线性插值与最邻近插值的时间复杂度相对较低

## 图像文件格式
一般的图像文件格式使用的是 Unsigned 8bits，CvMat矩阵对应的参数类型就是
CV_8UC1，CV_8UC2，CV_8UC3（最后的1、2、3表示通道数，譬如RGB3通道就用CV_8UC3）
而float 是32位的，对应CvMat数据结构参数就是：CV_32FC1，CV_32FC2，CV_32FC3...
double是64bits，对应CvMat数据结构参数：CV_64FC1，CV_64FC2，CV_64FC3等。

## 坐标
一行是同一个y row == height == Point.y
一列是同一个x col == width  == Point.x


# 直方图
## 直方图信息
    cv2.calcHist([img],[0],None,[256],[0,256])
参数
1.images:这是uint8或者float32的原图。应该是方括号方式传入：[img]
2.channels:也是用方括号给出的，我们计算histogram的channel的索引，灰度图：[0]，对于彩色图片：[0],[1]和[2]
3.mask：掩图，整个图像的histogram传入"None"。求特定区域图片的得创建一个mask
4.histSize：BIN数量，对于全刻度，我们传入[256].
5.ranges：RANGE，一般来说是[0,256].
返回值： 灰度图会返回一个256x1数组

    hist,bins=np.histogram(img.ravel(),256,[0,256])
Numpy计算bins是0-0.99,1-1.99，所以最后的范围是255-255.99.要表示这个需要加上256

    np.bincount()
比np.histogram()要快10倍，opencv更快

    matplotlib.pyplot.hist(img.ravel(),256,[0,256])
计算并画出直方图,对于BGR图可以如下画出
    histr = cv2.calcHist([img],[i],None,[256],[0,256])
    plt.plot(histr,color = col)

# 均衡
## 直方图归一化
一个好的图片应该是有所有范围都有像素分布，所以我们需要把histogram拉伸到两端，这就是histogram均衡，一般是用来提升图片的对比度。
    cv2.equalizeHist(img)
equalizeHist考虑的是图片全部对比度，对比度受限自适应直方图均衡
    clahe = cv2.createCLAHE(clipLimit=2.0, tileGridSize=(8,8))
    cl1 = clahe.apply(img)

# 轮廓

# 分割
## GrabCut


# 滤波
对于一维信号，图片可以被多种低通滤波器(LPF)，高通滤波器(HPF）过滤，一个LPF可以用在移除噪点，或者模糊图片。HPF可以用在找图片里找到边界。
## 低通
1. cv2.blur() cv2.boxFilter()
平均滤波，制定核的宽和高
2. 高斯滤波
blur = cv2.GaussianBlur(img,(5,5),0)
指定核的宽度和高度，应该是正数和奇数。我们也应该指定X和Y方向的标准偏差sigmaX和sigmaY。如果只有sigmaX被指定，sigmaY就和sigmaX一样。如果两个都是0，它们从核的大小里计算得出。
3. 中值滤波
blur = cv2.medianBlur(img,5)
4. 双边滤波
不是模糊边界的，在保持边界的情况下去除噪点
blur = cv2.bilateralFilter(img,9,75,75)

## 高通


# 二值化
    cv2.threshold(img, 127, 255, cv2.THRESH_BINARY)
THRESH_BINARY THRESH_BINARY_INV THRESH_TRUNC THRESH_TOZERO THRESH_TOZERO_INV

    cv2.adaptiveThreshold(img, 255, cv2.ADAPTIVE_THRESH_MEAN_C,cv2.THRESH_BINARY, 11, 2)
在同一张图片里的不同区域可以有不同阈值。这会给我们多种光照下更好的结果

# 形态学
## 膨胀和腐蚀
形态变换是根据图片的形状进行的简单运算。一般被用在二值图像上。需要两个输入，一个原始图片，另一个是被叫做结构元素或者是核
两个基本的形态运算是腐蚀和膨胀dilate, 
cv2.erode(img,kernel)
cv2.dilate(img,kernel)
kernel默认是一个简单的3X3矩阵,getStructuringElement（）函数指明它的形状
1. 对于二值图像来说
腐蚀：核与其覆盖的图像部分做“与”操作，如果全为1，则该像素点为1，否则为0；也就是0容易得到，图像更多的地方变黑了，白色部分被腐蚀了
膨胀：核与其覆盖的图像部分做“与”操作，如果全为0，则该像素点为0，否则为1；也就是1容易得到，图像更多的地方变白了，白色部分膨胀了
2. 对于一个灰度图像来说：
腐蚀：某一点的像素值，就是核与图像该部分像素值差的最小值。所以像素值变低比较容易，亮色部分被腐蚀。
膨胀：某一点的像素值，就是核与图像该部分像素值和的最大值。所以像素值变高比较容易，亮色部分膨胀。

## morphologyEx
其他的变形如开，闭，梯度基于腐蚀和膨胀
cv2.morphologyEx(img, cv2.MORPH_OPEN, kernel)
1.开运算 先腐蚀后膨胀
作用：放大裂缝和低密度区域，消除小物体，在平滑较大物体的边界时，不改变其面积

2.闭运算 MORPH_CLOSE 先膨胀后腐蚀
作用：排除小型黑洞，突触了比原图轮廓区域更暗的区域

3.形态学梯度 MORPH_GRADIENT   形态学梯度=膨胀图-腐蚀图 
作用：保留图像边缘
4.顶帽（礼帽）MORPH_TOPHAT 顶帽=原图-开运算    
作用：分离邻近点亮一些的斑块，进行背景提取
5.黑帽 MORPH_BLACKHAT  黑帽=闭运算-原图 
作用：用来分离比邻近点暗一些的斑块

# 基础
## mask
想要的区域是白色（255）而其他地方是黑色（0）

## 颜色
cv2.cvtColor(), cv2.inRange()

## 形状

## 加边框
cv2.copyMakeBorder()
* src - 输入图片
* top, bottom, left, right - 各个方向的边框像素宽度
* borderType - 标志位，定义要加什么样的边框
