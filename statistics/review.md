# Review

## Classical Categories:

![](<../.gitbook/assets/image (1) (2).png>)

* Supervised Learning: **Given labels**
  * Regression: 定量
    * Linear: Wage \~ age, education level
    * Non-linear
  * Classification: 定性（男女，ABC类，Y/N）
    * Bayes Classification
    * [KNN](https://app.gitbook.com/@hlj12530/s/stemgene/\~/drafts/-M6g39ffquVIlwbKwRop/statistics/knn)
  * KNN和Boosting既可以Regression，又可以Classification
* Unsupervised Learning: **Unknown labels**
  * Clustering: 基因表达，基于变量 $$x_1, x_2, ...,x_n$$ 将observation归入不同的群

## Prediction & Inference

**用观测数据去代表真实数据。**对于同一个线性回归的项目，10个数据集会产生10条不同的回归线，其中每一条都与真实值有些许区别，真实值是观察不到的，但却可以通过最小二乘去估计出参数。就如同随机变量的总体均值，我们不知道总体均值是什么，但可以用样本均值去代表。当用观测值去估计真实值时，有时高有时低，但当采样足够大，结果会非常接近真实值，这就是**无偏估计**。

* Prediction: $$\hat{Y}=\hat{f}(X)+\epsilon$$ ，由X推导$$\hat{Y}$$，不太关注$$\hat{f}$$具体的内容
* Inference：研究$$\hat{Y}和\hat{f}(X)$$的关系，如Y和X是否相关？哪个X对Y的影响更大？改变哪个X可以改变Y
  * 如果建模的主旨是inference，采用**线性模型**这种结构限定的模型的解释性Interpretability比较强，更容易理解Y随着某些X变化的关系，而且往往可以得到更精确的结果，因为对抗overfitting. 这个限定性或曲线的光滑度即是**自由度degree of freedom**，限定性强且曲线平坦的模型比锯齿形曲线具有更小的自由度。

![不同方法对应的解释性和适配性](<../.gitbook/assets/image (13).png>)

## Estimate $$\hat{f}$$

* 参数法，如 $$f(X)=\beta_0+\beta_1X_1+\beta_2X_2+...+\beta_pX_p$$&#x20;
  * Advantage: 由于预估出参数模型，用较少的训练样本可以拟合函数 $$f(X)$$&#x20;
  * Disadvantage: 很多情况下，无法用参数和变量之间的关系来表达出具体的函数形式，或者估计的 $$f$$ 形式与真实的存在较大差异。
* 非参数法，不需要事先估计$$f$$的形式
  * Advantage: Don't need to know $$f$$
  * Disadvantage: need more data

## Evaluation

无论是Regression和Classification，选择合适的光滑水平是成功建模的关键，需要权衡Bias-Var以及导致测试误差产生的U形曲线。

### Regression:&#x20;

* Mean Square Error: $$MSE=\frac{1}{n} \sum_{i=1}^{n}(y_i-\hat{f}(x_i))^2$$&#x20;

![统计学基本特征：当增加自由度，training error降低而testing error不一定降低](https://firebasestorage.googleapis.com/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M6ArfyS6R2h2Ac740eW%2Fuploads%2FtfQdFELOfGJQOvGwOoHu%2Ffile.png?alt=media)

* Tradeoff of Variance and Bias

$$E(y_0-\hat{f}(x_0))^2=Var(\hat{f}(x_0))+[Bias(\hat{f}(x_0))]^2+Var(\epsilon)$$ 最小化拟合的期望可以通过三项，其中$$Var(\epsilon)$$是不可约的，代表着模型的最佳标准，所以需要在$$\hat{f}(x_0)$$的方差和偏差中作出平衡

* 方差$$Var(\hat{f}(x_0))$$：对于适配不同的数据集，估计函数所产生的改变量。如果Var大，训练数据集微小的变化会导致估计函数较大的改变。自由度高有更大的方差。对于线性模型，如果自由度太大的话，Var会快速增加
* 偏差$$Bias(\hat{f}(x_0))$$：估计函数$$\hat{f}(x_0)$$本身和真实函数的误差，因为现实的模型几乎不是线性的，所以一般来说，自由度越高的方法所产生的偏差越小。对于非线性模型，稍微增加一些自由度，其Bias会迅速降低

![](<../.gitbook/assets/image (8).png>)

### Classification

误差为：$$\frac{1}{n}\sum_{i=1}^{n}I(y_0\neq \hat{y_0})$$&#x20;

其中 $$I(y_0\neq \hat{y_0})$$ 表示一个示性变量(indicator variable)，当 $$y_0\neq \hat{y_0}$$ 时$$I(y_0\neq \hat{y_0})=1$$，当$$y_0=\hat{y_0}$$时$$I(y_0\neq \hat{y_0})=0$$

#### Bayes Classifier贝叶斯分类器（类似不可约误差，无法达到）：

条件概率$$Pr(Y=j|X=x_0)$$，给定了观测向量$$X=x_0$$条件下$$Y=j$$的概率，如在二分类下，$$Pr(Y=1|X=x_0)>0.5$$，就将该观测的类别预测为1，否则为0。

贝叶斯错误率： $$1-E(maxPr(Y=j|X)$$ 其中期望平均了所有X可能值上的概率。这种作用在test set上的错误率是最低的。

因为很难知道给定X后Y的条件分布，所以是难以达到的黄金标准

#### [KNN的错误率](https://app.gitbook.com/@hlj12530/s/stemgene/\~/drafts/-M6g\_ZugJIj5OegHlipg/statistics/knn)

KNN可以产生对最优贝叶斯分类器近似的分类器。

![](<../.gitbook/assets/image (27).png>)

当1/K增加时，方法的柔性增强，training error会持续递减，但test error显示U形

