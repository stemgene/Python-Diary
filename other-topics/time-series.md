---
description: >-
  https://otexts.com/fppcn/components.html,
  https://online.stat.psu.edu/stat510/lesson/1/1.2
---

# Time Series

## 时间序列数据

![](../.gitbook/assets/image%20%2873%29.png)

## Time Series Preprocessing

### Missing values

[没有完美的数据插补法，只有最适合的](https://cloud.tencent.com/developer/article/1366604)

[python实现时序数据缺失值的插值](https://blog.csdn.net/weixin_43994085/article/details/105727060)

[【Python数据分析基础】: 数据缺失值处理](https://juejin.im/post/5b5c4e6c6fb9a04f90791e0c)

[数据分析之Pandas缺失数据处理](https://blog.csdn.net/Datawhale/article/details/107096422)

[Working with missing data](https://pandas-docs.github.io/pandas-docs-travis/user_guide/missing_data.html#interpolation)

{% embed url="https://pd.DataFrame.interpolate" %}

[scipy.interpolate](https://docs.scipy.org/doc/scipy/reference/tutorial/interpolate.html)

[插值interpolate模块](https://www.jianshu.com/p/b306095309db)

## 时间序列组成

### 常用模型

![](../.gitbook/assets/image%20%2878%29.png)

假设一条时间序列是由多种成分相加得来，那么它可以写为如下形式： $$y_t=S_t+T_t+R_t$$ ,在上式中 $$ y_t$$ 表示时间序列数据，$$S_t$$ 表示季节项， $$T_t$$ 表示趋势-周期项， $$R_t$$ 表示残差项。此外，时间序列也可以写成相乘的形式： $$y_t=S_t×T_t×R_t$$ 

如果季节性波动的幅度或者趋势周期项的波动不随时间序列水平的变化而变化，那么加法模型是最为合适的。当季节项或趋势周期项的变化与时间序列的水平成比例时，则乘法模型更为合适。在经济时间序列中，乘法模型较为常用。

使用乘法分解的一种替代方法是：首先对数据进行变换，直到时间序列随时间的波动趋于稳定，然后再使用加法分解。显然，采用对数变换的加法模型$$logy_t=logS_t+logT_t+logR_t.$$等价于乘法模型：$$y_t=S_t×T_t×R_t$$ 

### Decompose

将数据拆分为三种状态：trend, seasonality and residuals。Residuals是稳定的数据，是我们所需要的

![](../.gitbook/assets/image%20%2882%29.png)

## Stationary

因为ARIMA模型要求数据是稳定的，需要先判断数据是否稳定。

Stationary Criterion:

* The mean is constant
* The variance is constant
* The autocorrelation is constant

![](https://lh3.googleusercontent.com/Q_LIXKyBYLUgCgniY5-nxeSQKIPHT_Zitr7kw6YPYZrmlUeygR9GvJbLNKcbYlkxaURBz0Y3Jkdz4M0m9xr-a_-jC_xFbAQvyUDM7oYplKSJKcl62wu7WB4Z9fWDgY6maqNDdC2gOg8)

第一行左图数据的均值对于时间轴来说是常量，即数据的均值不是时间的函数，右图数值的整体趋势是增加的，所以均值是时间的函数，数据具有趋势，所以不是稳定的

第二行左图数据的方差对于时间是常量，右图的振幅在不同时间点不一样，但左右图的均值是一致的。

第三行是一个时序数据的自协方差，就是它在不同两个时刻i，j的值的协方差，左图的自协方差于时间无关，右图随着时间不同、数据的波动频率不同，导致它i，j取值不同，就会得到不同的协方差，因此也是非稳定的。

### 判断stationary

* Rolling statistic --即每个时间段内的平均数据均值和标准差情况，如下图的rolling均值/标准差具有越来越大的趋势，是不稳定的
* Dickey-Fuller Test。通过假设检验

![](../.gitbook/assets/image%20%2879%29.png)

### Make stational

不稳定的原因主要有两类

* trend
  * 聚合：将时间轴缩短，以一段时间内月/年的均值作为数据值。使不同的时间段内的值差距缩小。
  * 平滑：以一个滑动窗口内的均值代替原来的值，使值之间的差距缩小
  * 多项式过滤：用一个回归模型来拟合现有数据，使数据平滑
* Seasonality
  * 差分化：以特定滞后数目的时刻的值做差
  * 分解：对趋势和季节性分别建模再移除它们

由于原数据值域范围比较大，为了缩小值域，同时保留其他信息，常用的方法是**对数化**，取log。

## Autocorrelation and Partial Autocorrelation

[自相关与偏自相关的简单介绍](http://www.atyun.com/4462.html)

## Prediction

首先确定p，d，q的参数

可以比对AR，MA和ARIMA三种模型的RSS，选择最小的说明拟合度最好。

用数据带入模型进行预测

参考：

{% embed url="https://1.时序数据的分析" %}

2.[python时间序列ARIMA的实现及原理（预测茅台股票数据\)](https://blog.csdn.net/qq_36523839/article/details/80191243)

3.[使用ARIMA进行时间序列预测（Python）](https://www.biaodianfu.com/time-series-forecasting-with-arima-in-python.html), [时间序列建模完整教程（R语言）](https://www.biaodianfu.com/complete-tutorial-time-series-modeling.html)

{% embed url="https://4.Python实现时间序列分析" %}

5.Kaggle: [Everything you can do with a time series](https://www.kaggle.com/thebrownviking20/everything-you-can-do-with-a-time-series/notebook#3.-Time-series-decomposition-and-Random-walks)



