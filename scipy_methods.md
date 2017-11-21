# scipy.sparse
* bsr_matrix(arg1[, shape, dtype, copy, blocksize]) Block Sparse Row matrix
coo_matrix是三元组，不能按行也不能按列切片
* coo_matrix(arg1[, shape, dtype, copy]) A sparse matrix in COOrdinate format.
* csc_matrix(arg1[, shape, dtype, copy]) Compressed Sparse Column matrix
to_csc 是按列压缩的稀疏矩阵，按列切片比较快，可以按行切片

* csr_matrix(arg1[, shape, dtype, copy]) Compressed Sparse Row matrix
to_csr  是按行压缩的稀疏矩阵，按行切片比较快，可以按列切片

* dia_matrix(arg1[, shape, dtype, copy]) Sparse matrix with DIAgonal storage
* dok_matrix(arg1[, shape, dtype, copy]) Dictionary Of Keys based sparse matrix.
* lil_matrix(arg1[, shape, dtype, copy]) Row-based linked list sparse matrix

## 操作
* A = coo_matrix(array)
* A.toarray()
* 可以用hstack,vstack合并相同数据类型的两个稀疏矩阵
* （似乎)除了coo之外稀疏矩阵的存储格式，都可以进行slice操作 
* sparce矩阵的读取。可以像常规矩阵一样通过下标读取。也可以通过getrow(i)，gecol(i)读取特定的列或者特定的行，以及nonzero()读取非零元素的位置。

