 # 语法
## 图片
\usepackage{graphicx}
\includegraphics[height=高度]{图片文件名} 
或者: \includegraphics[width=宽度]{图片文件名}
\includegraphics[height=高度][angle=旋转角度]{图片文件名}
其中的"高度"和"宽度"是指希望图片打印的高度和宽度, 必须给出单位, 可用厘米(cm)或英寸(in)
\begin{figure}[htbp]
\centering\includegraphics[width=3.5in]{fig}
\caption{something}\label{fig:1}
\end{figure}

## 矩阵
### []
$A=\begin{bmatrix}
1&3 \\
3&3
\end{bmatrix}$

## 表格

##符号
* \sqrt 平方根（square root），n 次方根相应地为: \sqrt[n]
* \vec 向量
* \int 积分运算符（integral operator）
* \prod 乘积运算符（product operator）
* \leqslant \leq 小于等于 \geqslant \geq 大于等于 
* \infty 无穷
* \sum\limits_{n = 0}^\infty 求和 上下标

## 格式
* \overline 和\underline 在表达式的上、下方画出水平线
* \widetilde 加波浪线
* \hat  或 \widehat 加^号
* \dot{要加点的字母}加一个点 \ddot{要加点的字母} 加两个点
* \mathbf{}
* \overbrace 和\underbrace 在表达式的上、下方给出一水平的大括号
* \overrightarrow 和\overleftarrow 上方箭头

# 模板
## word模板
\documentclass[UTF8]{ctexart}
\usepackage{amsmath}
\usepackage{amssymb}
\usepackage{geometry}
\usepackage{graphicx}
\usepackage{forest,adjustbox}
\geometry{left=2.5cm,right=2.5cm,top=0.5cm,bottom=2.5cm}
\title{}
\author{}
\date{}
\begin{document}
\maketitle
\section{}

\end{document}

## ppt模板
