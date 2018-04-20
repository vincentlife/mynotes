# basic
## file
pyx 文件 (可在pycharm Editor filetypes中添加)
## 变量
cdef：
    int i, *j, k[100]
    cdef struct node:
        int key
        float value
    bint flag
cdef enum:
    const = 1
ctypedef来定义类型名称:
ctypedef long long LL

## 函数
* def: 传入python对象，返回python对象，直接调用
* cdef: 传入python对象或C/C++值，返回python对象或C/C++值，不可直接调用
* cpdef: 以上两者的混合
注意:
+ 只有def和cpdef定义的函数在编译后可以在python代码中直接调用，cdef定义的函数则不能。 可以使用def来对外封装:
+ cdef报错不能很好的捕获异常。可以这样使用
    cdef int divide(int x, int y) except 0:
出错将返回0
+ 只有作为函数参数时 类型前面的cdef可以省略

# c wrapper