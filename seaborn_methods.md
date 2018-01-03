# PairMap

# tips
## 中文字体显示
import matplotlib as mpl
mpl.rcParams['font.sans-serif'] = ['Microsoft YaHei'] #指定默认字体  
mpl.rcParams['axes.unicode_minus'] = False # 解决保存图像是负号'-'显示为方块的问题
sns.axes_style()，可以看到是否成功设定字体为微软雅黑