# Cluster

{% embed url="https://blog.csdn.net/sinat_26917383/article/details/51611519" %}

[https://blog.csdn.net/jinping\_shi/article/details/52433975](https://blog.csdn.net/jinping\_shi/article/details/52433975)

**Cluster:** Finding groups of objects such that the objects in a group will be similar (or related) to one another and different from (or unrelated to) the objects in other groups. **Minimize intra-cluster distance, maximize inter-cluster distance**

![](<../.gitbook/assets/image (70).png>)

## **Distance & Norm:**

### 样本之间的距离

向量的范数可以简单形象的理解为向量的长度，或者向量到零点的距离，或者相应的两个点之间的距离||x||，满足非负性||x|| >= 0，齐次性||cx|| = |c| ||x|| ，三角不等式||x+y|| <= ||x||

* Manhattan Distance & L1 Norm: 在平面上，坐标（x1, y1）的点P1与坐标（x2, y2）的点P2的曼哈顿距离为：![](https://img-my.csdn.net/uploads/201211/20/1353398955\_7627.png)对于线性回归模型，使用L1正则化的模型建叫做Lasso回归。L1正则化是指权值向量w中各个元素的绝对值之和，可以产生稀疏权值矩阵（稀疏矩阵指的是很多元素为0，只有少数元素是非零值的矩阵，即得到的线性回归模型的大部分系数都是0. ），即产生一个稀疏模型增加稀疏性，可以用于特征选择。
* Euclidean distance欧式距离 & L2 Norm： $$d = \sqrt{\sum{(x_{it}-x_{jt})^2}}$$ ，使用L2正则化的模型叫做Ridge回归（岭回归）。L2正则化是指权值向量w中各个元素的平方和然后再求平方根，可以防止模型过拟合（overfitting）；一定程度上，L1也可以防止过拟合。
* 切比雪夫距离，若二个向量或二个点x1和x2，其坐标分别为(x11, x12, x13, ... , x1n)和(x21, x22, x23, ... , x2n)，则二者的切比雪夫距离为：d = max(|x1i - x2i|)，i从1到n。对应L∞范数。
* Minkowski Distance：一组距离的定义。对应Lp范数，p为参数。当p=1时，就是曼哈顿距离，当p=2时，就是欧氏距离，当p→∞时，就是切比雪夫距离。
* 马氏距离
* 余弦距离： $$cos\theta=\frac{\sum{A_i*B_i}}{\sqrt{\sum{A_i^2}}*\sqrt{\sum{B_i^2}}}$$&#x20;

聚类分析的数据都会进行标准化，**标准化是因为聚类数据会受数据的量纲影响。**Minkowski距离受量纲影响较大。马氏距离受量纲影响较小，还有cos(余弦相似性)余弦值的范围在\[-1,1]之间，值越趋近于1，代表两个向量的方向越趋近于0，他们的方向更加一致。相应的相似度也越高（cos距离可以用在文本挖掘，文本词向量距离之上）。

### 类与类之间的距离：

一个点集，群落，如何定义群体距离。一般有以下几种距离。

![](<../.gitbook/assets/image (67).png>)

## Popular cluster methods:

### K-means:

K-Means 聚类(MacQueen, 1967)是以样本间距离为基础，将所有的观测之间划分到K个群体，使得群体和群体之间的距离尽量大，同时群体内部的观测之间的“距离和”最小。Each cluster is associated with a centroid (center point) , Each point is assigned to the cluster with the closest centroid, K need to be specified.

1. Select K points as the initial centroids.
2. Repeat&#x20;
   1. Form K clusters by assigning all points to the closest centroid
   2. Recompute the centroid of each cluster
3. until The centroids don't change

![](<../.gitbook/assets/image (69).png>)

K均值算法通常在前几个iteration中就收敛converge

* 对outlier或异常值很敏感。数据点在数据空间上的密度扩展具有差异、数据点为非凹形状的情况下，K均值聚类算法的运行结果不佳。
