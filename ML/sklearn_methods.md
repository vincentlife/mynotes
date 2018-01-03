# sklearn.metrics
## scoring 
### Classification       
* ‘accuracy’  metrics.accuracy_score   
* ‘average_precision’ metrics.average_precision_score  
* ‘f1’    metrics.f1_score    for binary targets
* ‘f1_micro’  metrics.f1_score    micro-averaged
* ‘f1_macro’  metrics.f1_score    macro-averaged
* ‘f1_weighted’   metrics.f1_score    weighted average
* ‘f1_samples’    metrics.f1_score    by multilabel sample
* ‘neg_log_loss’  metrics.log_loss    requires predict_proba support
* ‘precision’ etc.    metrics.precision_score suffixes apply as with ‘f1’
* ‘recall’ etc.   metrics.recall_score    suffixes apply as with ‘f1’
* ‘roc_auc’   metrics.roc_auc_score    

## 聚类       
* ‘adjusted_mutual_info_score’    metrics.adjusted_mutual_info_score   
* ‘adjusted_rand_score’   metrics.adjusted_rand_score  
* ‘completeness_score’    metrics.completeness_score   
* ‘fowlkes_mallows_score’ metrics.fowlkes_mallows_score    
* ‘homogeneity_score’ metrics.homogeneity_score    
* ‘mutual_info_score’ metrics.mutual_info_score    
* ‘normalized_mutual_info_score’  metrics.normalized_mutual_info_score     
* ‘v_measure_score’   metrics.v_measure_score  
      
## 回归
### 可释方差值
metrics.explained_variance_score 
explained_variance_score(y_true, y_pred, multioutput= ) 

### 平均绝对误差 MAE
    ‘neg_mean_absolute_error’  
    metrics.mean_absolute_error
mean_absolute_error(y_true, y_pred, multioutput='raw_values')

### 均方误差（Mean squared error） 
    ‘neg_mean_squared_error’    
    metrics.mean_squared_error  

###  中值绝对误差（Median absolute error）
    ‘neg_median_absolute_error’ 
    metrics.median_absolute_error    
median_absolute_error(y_true, y_pred) 
对异类（outliers）的情况是健壮的。该loss函数通过计算target和prediction间的绝对值，然后取中值得到。median_absolute_error不支持multioutput。

###  R方值，确定系数      
* ‘r2’    metrics.r2_score

## others
一些metrics不在scoring中提供，因为它可能需要额外参数,通过make_scorer来构造scorer传给scoring参数使用

	from sklearn.metrics import fbeta_score, make_scorer
	ftwo_scorer = make_scorer(fbeta_score, beta=2)
可以构造自己的评价函数，接收预测list和真实list两个参数
可以构造自己的scoring object 接收(estimator, X, y)

查看各个类别的情况
classification_report(y_true, y_pred, target_names=target_names)

# sklearn.externals.joblib
from sklearn.externals.joblib import dump,load

dump(grid_search, 'grid_search.dmp', compress=3)
第三个参数为压缩级别，0为不压缩，3为合适的压缩级别

grid_search = load('grid_search.dmp')

# sklearn.feature_selection
