# GBDT 调参
一般GBDT调参首先确定 n_estimators，主要与learning_rate有关
调参步骤：
1. 设定基础参数{parm0}，基础评判指标{metrics0}；
2. 在训练集上做cross-validation，做训练集/交叉验证集上偏差/方差与树棵树的关系图；
3. 判断模型是过拟合 or 欠拟合，更新相应参数{parm1}；
4. 重复2、3步，确定树的棵树n_estimators；
5. 采用参数{parm1}、n_estimators，训练模型，并应用到测试集


## lightgbm调参

与大多数使用depth-wise tree算法的GBM工具不同，由于LightGBM使用leaf-wise tree算法，因此在迭代过程中能更快地收敛；但leaf-wise tree算法较容易过拟合；为了更好地避免过拟合，请重点留意以下参数:

1. num_leaves. 这是控制树模型复杂性的重要参数。理论上，我们可以通过设定num_leaves = 2^(max_depth) 去转变成为depth-wise tree。但这样容易过拟合，因为当这两个参数相等时, leaf-wise tree的深度要远超depth-wise tree。因此在调参时，往往会把 num_leaves的值设置得小于2^(max_depth)。例如当max_depth=6时depth-wise tree可以有个好的准确率，但如果把 num_leaves 设成 127 会导致过拟合，要是把这个参数设置成 70或 80 却有可能获得比depth-wise tree有更好的准确率。事实上，当我们用 leaf-wise tree时，我们可以忽略depth这个概念，毕竟leaves跟depth之间没有一个确切的关系。

2. min_data_in_leaf.或min_child_samples 默认值20. 这是另一个避免leaf-wise tree算法过拟合的重要参数。该值受到训练集数量和num_leaves这两个值的影响。把该参数设的更大能够避免生长出过深的树，但也要避免欠拟合。在分析大型数据集时，该值区间在数百到数千之间较为合适。

3. max_depth.  限制树算法生长过深。默认值为-1 即不限制

### 提高速度的参数
· 通过设定bagging_fraction和bagging_freq来使用 bagging算法 分别对应 subsample 和 subsample_freq
· 通过设定 feature_fraction来对特征采样 对应colsample_bytree
· 设定更小的max_bin值
· 使用save_binary 以方便往后加载数据的速度
· 设定n_jobs计算参数

### 提高精度的参数
· 设定更大的max_bin值(但会拖慢速度)
· 设定较小的learning_rate值，较大的num_iterations值
· 设定更大的num_leaves值(但容易导致过拟合)
· 加大训练集数量（更多样本，更多特征）
· 试试boosting= dart

### 避免过拟合的参数
· 设定较小的max_bin
· 设定更小的num_leaves
· 设定min_data_in_leaf和min_sum_hessian_in_leaf
· 通过设定bagging_fraction和bagging_freq来使用 bagging算法
· 通过设定feature_fraction来对特征采样。
· 加大训练集数量（更多样本，更多特征）
· 通过设定lambda_l1, lambda_l2以及min_gain_to_split来采取正则化措施
· 通过设定max_depth以避免过拟


## xgboost调参



# ridge lasso 回归
alpha 为正则化项参数，值越大说明模型偏离线性模型越远

# random forest
调参