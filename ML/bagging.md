# basic
随机采样(bootsrap)就是从训练集里面采集固定个数的样本，但是每采集一个样本后，都将样本放回。也就是说，之前采集到的样本在放回后有可能继续被采集到。对于Bagging算法，一般会随机采集和训练集样本数m一样个数的样本。这样得到的采样集和训练集样本的个数相同，但是样本内容不同。如果我们对有m个样本训练集做T次的随机采样，，则由于随机性，T个采样集各不相同。

注意到这和GBDT的子采样是不同的。GBDT的子采样是无放回采样，而Bagging的子采样是放回采样。
对于一个样本，它在某一次含m个样本的训练集的随机采样中，每次被采集到的概率是1/m。不被采集到的概率为1−1m。如果m次采样都没有被采集中的概率是(1−1m)m。当m → ∞时，(1−1/m)^m →1e≃0.368。也就是说，在bagging的每轮随机采样中，训练集中大约有36.8%的数据没有被采样集采集中。

对于这部分大约36.8%的没有被采样到的数据，我们常常称之为袋外数据(Out Of Bag, 简称OOB)。这些数据没有参与训练集模型的拟合，因此可以用来检测模型的泛化能力。在sklearn里面oob_score=True


# random forest