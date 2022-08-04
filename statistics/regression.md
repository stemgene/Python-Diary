# Regression

Regression analysis is a set of statistical processes for estimating the relationships between a dependent variable and one or more independent variables

![](https://lh3.googleusercontent.com/bsA-0zKmivimkFVPDw3Dt9T7P9wsmrb6Ajy8GAk1c-sELDTPe0DqC1o14Cmh8pwAmTadp7zLQ2NV3Po3XoFCEctv2CJ0bb9-94Fc5Qo5mkILiULDVCcync7xNd6UN8OWzaGLKpfnd7E)

## Evaluation

无论是Regression和Classification，选择合适的光滑水平是成功建模的关键，需要权衡Bias-Var以及导致测试误差产生的U形曲线。

### MSE

* Mean Square Error: $$MSE=\frac{1}{n} \sum_{i=1}^{n}(y_i-\hat{f}(x_i))^2$$&#x20;

![统计学基本特征：当增加自由度，training error降低而testing error不一定降低](https://firebasestorage.googleapis.com/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M6ArfyS6R2h2Ac740eW%2Fuploads%2FyGZ2lp8buiOCzqb4vWv6%2Ffile.png?alt=media)

* Tradeoff of Variance and Bias

$$E(y_0-\hat{f}(x_0))^2=Var(\hat{f}(x_0))+[Bias(\hat{f}(x_0))]^2+Var(\epsilon)$$ 最小化拟合的期望可以通过三项，其中$$Var(\epsilon)$$是不可约的，代表着模型的最佳标准，所以需要在$$\hat{f}(x_0)$$的方差和偏差中作出平衡

* 方差$$Var(\hat{f}(x_0))$$：对于适配不同的数据集，估计函数所产生的改变量。如果Var大，训练数据集微小的变化会导致估计函数较大的改变。自由度高有更大的方差。对于线性模型，如果自由度太大的话，Var会快速增加
* 偏差$$Bias(\hat{f}(x_0))$$：估计函数$$\hat{f}(x_0)$$本身和真实函数的误差，因为现实的模型几乎不是线性的，所以一般来说，自由度越高的方法所产生的偏差越小。对于非线性模型，稍微增加一些自由度，其Bias会迅速降低

![](<../.gitbook/assets/image (8).png>)

### $$R^2$$&#x20;

&#x20;$$R^2$$ is a statistical measure of how close the data are to the fitted regression line.

$$R^2=1-\frac{SS_{residuals}}{SS_{total}}=1-\frac{\sum_i{(y_i-\hat{y_i})^2}}{\sum_i{(y_i-\bar{y_i})^2}}$$&#x20;

* Range between \[0, 1]: a higher value suggests for a better model fit.
* Limitation: sensitive to independent variable (IV) and dependent variable (DV). 如果要比较$$R^2$$, 前提条件需要为具有相同的IV和DV

Adjusted $$R^2$$: it compares the explanatory power of regression models with different number of IVs; can be negative

$$Adj R^2=1-\frac{SS_{residuals}/(n-K)}{SS_{total}/(n-1)}=1-\frac{\sum_i{(y_i-\hat{y_i})^2}/(n-K)}{\sum_i{(y_i-\bar{y_i})^2}/(n-1)}$$

