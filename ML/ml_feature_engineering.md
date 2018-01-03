# Exploratory Data Analysis

# Feature Engineering
## Preprocessing

# Pipeline
Pipleline中最后一个之外的所有estimators都必须是变换器（transformers），最后一个estimator可以是任意类型（transformer，classifier，regresser）
如果最后一个estimator是个分类器，则整个pipeline就可以作为分类器使用，其他同理。

## estimator获取
pipe.steps[0]
pipe.named_steps['pca']

## 参数
在pipeline中estimator的参数通过使用<estimator>__<parameter>
语法来获取比如pipe.set_params(clf__C=10)
可以进行调参，包括estimator本身, 
params=dict(pca=[None,PCA(5),PCA(10)],clf=[SVC(),LogisticRegression()],
            clf_C=[0.1,10,100])
grid_research=GridSearchCV(pipe,param_grid=params)

## make_pipeline
接受可变数量的estimators并返回一个pipeline，每个estimator的名称自动填充
make_pipeline(Binarizer(),MultinomialNB())


# feature Union

## Feature

# score
## basic
* True Positive （真正, TP）被模型预测为正的正样本；
* True Negative（真负 , TN）被模型预测为负的负样本 ；
* False Positive （假正, FP）被模型预测为正的负样本；
* False Negative（假负 , FN）被模型预测为负的正样本；
* True Positive Rate（真正率 , TPR）或灵敏度（sensitivity） 
   TPR = TP /（TP + FN） 
   正样本预测结果数 / 正样本实际数
* True Negative Rate（真负率 , TNR）或特指度（specificity） 
   TNR = TN /（TN + FP） 
   负样本预测结果数 / 负样本实际数 
* False Positive Rate （假正率, FPR） 
   FPR = FP /（FP + TN） 
   被预测为正的负样本结果数 /负样本实际数 
* False Negative Rate（假负率 , FNR） 
   FNR = FN /（TP + FN） 
   被预测为负的正样本结果数 / 正样本实际数

## sklearn
sklearn提供如下scorer，error越小越好，score越大越好
* median_absolute_error
* r2
* recall_micro
* roc_auc
* adjusted_rand_score
* recall_samples
* recall_macro
* average_precision
* precision_samples
* f1_samples
* mean_absolute_error
* recall
* log_loss
* precision
* recall_weighted

## ROC,AUC
ROC曲线的横坐标为false positive rate（FPR），纵坐标为true positive rate（TPR）。曲线下方的面积即为AUC值。ROC曲线是通过调整二值分类器判定为正的概率的阈值来得到的。

* (0,1)，即FPR=0,所以FP（false positive）=0。 TPR=1，所以 FN（false negative）=0。这是一个完美的分类器，它将所有的样本都正确分类。
* (1,0)，即FPR=1，所以TN=0, TPR=0，所以TP=0。 成功避开了所有的正确答案。
* (0,0)，即FPR=TPR=0，即FP（false positive）=TP（true positive）=0，可以发现该分类器预测所有的样本都为负样本（negative）
* （1,1），同理，分类器实际上预测所有的样本都为正样本。
*  ROC曲线越接近左上角，该分类器的性能越好。
*  对角线上的点其实表示的是一个采用随机猜测策略的分类器的结果

### sklearn
from sklearn.metrics import roc_curve, roc_auc_score

# preprocess
### 特征选择
　　当数据预处理完成后，我们需要选择有意义的特征输入机器学习的算法和模型进行训练。通常来说，从两个方面考虑来选择特征：

+ 特征是否发散：如果一个特征不发散，例如方差接近于0，也就是说样本在这个特征上基本上没有差异，这个特征对于样本的区分并没有什么用。
+  特征与目标的相关性：这点比较显见，与目标相关性高的特征，应当优选选择。除方差法+外，本文介绍的其他方法均从相关性考虑。
　　根据特征选择的形式又可以将特征选择方法分为3种,我们使用sklearn中的feature_selection库来进行特征选择：

* Filter：过滤法，按照发散性或者相关性对各个特征进行评分，设定阈值或者待选择阈值的个数，选择特征。
* Wrapper：包装法，根据目标函数（通常是预测效果评分），每次选择若干特征，或者排除若干特征。
* Embedded：嵌入法，先使用某些机器学习的算法和模型进行训练，得到各个特征的权值系数，根据系数从大到小选择特征。类似于Filter方法，但是是通过训练来确定特征的优劣。

### 降维
常见的降维方法除了以上提到的基于L1惩罚项的模型以外，另外还有主成分分析法（PCA）和线性判别分析（LDA），线性判别分析本身也是一个分类模型。PCA和LDA有很多的相似点，其本质是要将原始的样本映射到维度更低的样本空间中，但是PCA和LDA的映射目标不一样：PCA是为了让映射后的样本具有最大的发散性；而LDA是为了让映射后的样本有最好的分类性能。所以说PCA是一种无监督的降维方法，而LDA是一种有监督的降维方法。

1. PCA降维：
from sklearn.decomposition import PCA  
#主成分分析法，返回降维后的数据，参数n_components为主成分数目
PCA(n_components=2).fit_transform(iris.data)
2. LDA降维
from sklearn.lda import LDA2 
#线性判别分析法，返回降维后的数据，参数n_components为降维后的维数
LDA(n_components=2).fit_transform(iris.data, iris.target)