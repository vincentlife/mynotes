# DMatrix
## construct
xgboost.DMatrix(data, label=None, missing=None, weight=None, silent=False, feature_names=None, feature_types=None, nthread=None)

data numpy.arrays
## object method
* num_col()
* num_row()
* save_binary(fname, silent=True)
* slice

# xgboost.train()
xgboost.train(params, dtrain, num_boost_round=10, evals=(), obj=None, feval=None, maximize=False, early_stopping_rounds=None, evals_result=None, verbose_eval=True, xgb_model=None, callbacks=None, learning_rates=None)

# xgboost.sklearn.XGBClassifier
## init
xgboost.XGBClassifier(max_depth=3, learning_rate=0.1, n_estimators=100, silent=True, objective='binary:logistic', booster='gbtree', n_jobs=1, nthread=None, gamma=0, min_child_weight=1, max_delta_step=0, subsample=1, colsample_bytree=1, colsample_bylevel=1, reg_alpha=0, reg_lambda=1, scale_pos_weight=1, base_score=0.5, random_state=0, seed=None, missing=None, **kwargs)

这里 n_estimators 即为num_round boosting迭代计算次数

## fit

## get_fscore
效果等同于


# xgboost.XGBRegressor


# xgboost.plot


# 参数
## 通用参数
1. booster[默认gbtree]
选择每次迭代的模型，有两种选择： 
gbtree：基于树的模型 
gbliner：线性模型

2. silent[默认0]

当这个参数值为1时，静默模式开启，不会输出任何信息。
一般这个参数就保持默认的0，因为这样能帮我们更好地理解模型。

3. nthread[默认值为最大可能的线程数]
这个参数用来进行多线程控制，应当输入系统的核数。如果你希望使用CPU全部的核，那就不要输入这个参数，算法会自动检测它。 

## booster参数
1. eta[默认0.3]
和GBM中的 learning rate 参数类似。
通过减少每一步的权重，可以提高模型的鲁棒性。
典型值为0.01-0.2。

2. min_child_weight[默认1]
决定最小叶子节点样本权重和。
和GBM的 min_child_leaf 参数类似，但不完全一样。XGBoost的这个参数是最小样本权重的和，而GBM参数是最小样本总数。
这个参数用于避免过拟合。当它的值较大时，可以避免模型学习到局部的特殊样本。
但是如果这个值过高，会导致欠拟合。这个参数需要使用CV来调整。

3. max_depth[默认6]
和GBM中的参数相同，这个值为树的最大深度。
这个值也是用来避免过拟合的。max_depth越大，模型会学到更具体更局部的样本。
需要使用CV函数来进行调优。
典型值：3-10

4. max_leaf_nodes
树上最大的节点或叶子的数量。
可以替代max_depth的作用。因为如果生成的是二叉树，一个深度为n的树最多生成n2个叶子。
如果定义了这个参数，GBM会忽略max_depth参数。

5. gamma[默认0]
在节点分裂时，只有分裂后损失函数的值下降了，才会分裂这个节点。Gamma指定了节点分裂所需的最小损失函数下降值。这个参数的值越大，算法越保守。这个参数的值和损失函数息息相关，所以是需要调整的。

6. max_delta_step[默认0]
这参数限制每棵树权重改变的最大步长。如果这个参数的值为0，那就意味着没有约束。如果它被赋予了某个正值，那么它会让这个算法更加保守。通常，这个参数不需要设置。但是当各类别的样本十分不平衡时，它对逻辑回归是很有帮助的。
这个参数一般用不到，但是你可以挖掘出来它更多的用处。

7. subsample[默认1]
和GBM中的subsample参数一模一样。这个参数控制对于每棵树，随机采样的比例。
减小这个参数的值，算法会更加保守，避免过拟合。但是，如果这个值设置得过小，它可能会导致欠拟合。典型值：0.5-1

8. colsample_bytree[默认1]
和GBM里面的max_features参数类似。用来控制每棵随机采样的列数的占比(每一列是一个特征)。
典型值：0.5-1 。

9. colsample_bylevel[默认1]
用来控制树的每一级的每一次分裂，对列数的采样的占比。
我个人一般不太用这个参数，因为subsample参数和colsample_bytree参数可以起到相同的作用。但是如果感兴趣，可以挖掘这个参数更多的用处。

10. lambda[默认1]
权重的L2正则化项。(和Ridge regression类似)。
这个参数是用来控制XGBoost的正则化部分的。虽然大部分数据科学家很少用到这个参数，但是这个参数在减少过拟合上还是可以挖掘出更多用处的。

11. alpha[默认1]
L1正则化项的权重。(和Lasso regression类似)。
可以应用在很高维度的情况下，使得算法的速度更快。

12. scale_pos_weight[默认1]
在各类别样本十分不平衡时，把这个参数设定为一个正值，可以使算法更快收敛。

## 学习目标参数
1. objective[默认reg:linear]
* “reg:linear” –线性回归。
* “reg:logistic” –逻辑回归。
* “binary:logistic” –二分类的逻辑回归问题，输出为概率。
* “binary:logitraw” –二分类的逻辑回归问题，输出的结果为wTx。
* “count:poisson” –计数问题的poisson回归，输出结果为poisson分布。在poisson回归中，max_delta_step的缺省值为0.7。(used to safeguard optimization)
* rank:pairwise –set XGBoost to do ranking task by minimizing the pairwise loss

* multi:softmax 让XGBoost采用softmax目标函数处理多分类问题，同时需要设置参数num_class（类别个数）

* multi:softprob –和softmax一样，但是输出的是ndata * nclass的向量，可以将该向量reshape成ndata行nclass列的矩阵。没行数据表示样本所属于每个类别的概率。

2. eval_metric[默认值取决于objective参数的取值]
可以添加多种评价指标，以list传递参数对给程序

* “rmse”: root mean square error
* “logloss”: negative log-likelihood
* “error”: Binary classification error rate. It is calculated as #(wrong cases)/#* (all cases). For the predictions, the evaluation will regard the instances with prediction value larger than 0.5 as positive instances, and the others as negative instances.
* “merror”: Multiclass classification error rate. It is calculated as #(wrong * cases)/#(all cases).
* “mlogloss”: Multiclass logloss
* “auc”: Area under the curve for ranking evaluation.
* “ndcg”:Normalized Discounted Cumulative Gain
* “map”:Mean average precision

# 调参步骤
第一步：确定学习速率和tree_based 参数调优的估计器数目
第二步： max_depth 和 min_weight 参数调优。 先对这两个参数调优，是因为它们对最终结果有很大的影响
第三步：gamma参数调优
第四步：调整subsample 和 colsample_bytree 参数
第五步：正则化参数调优。降低过拟合
第6步：降低学习速率 使用较低的学习速率，以及使用更多的决策树

