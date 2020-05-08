# Linear Regression

核心问题：对于$$f(X)=\beta_0+\beta_1X_1+\beta_2X_2+...+\beta_pX_p+\epsilon$$

* X与Y是否有关？
* X与Y的关系有多强，关系是否是线性的
* 哪个X与Y的关系更强
* 如何使X估计Y更精确
* 对未来的预测精度
* X之间是否协同

## Simple Linear Regression

对于$$Y=\beta_0+\beta_1X_1$$，估计出其系数得到$$\hat{Y}=\hat{\beta_0}+\hat{\beta_1}X_1$$

1. 根据变量X的第i个值，求出每一个估计值的残差 $$e_i=y_i-\hat{y_i}$$ 
2. 求residual sum of squares, $$RSS={e_1}^2+{e_2}^2+...+{e_n}^2$$ 
3. 用least square最小二乘法使RSS最小
4. 求出$$\hat{\beta_0}和\hat{\beta_1}$$

$$\hat{\beta_1}=\frac{\sum_{i=1}^{n}(x_i-\bar{x})(y_i-\bar{y})}{\sum_{i=1}^{n}(x_i-\bar{x})}$$ ，$$\hat{\beta_0}=\hat{y}-\hat{\beta_1}\bar{x}$$。其中 $$\bar{y}=\frac{1}{n}\sum{y_i}$$，$$\bar{x}=\frac{1}{n}\sum{x_i}$$是样本均值。

### **标准误差standard error：**

**SE功能1——计算置信区间：**用样本均值 $$\hat{\mu}$$ 估计总体均值 $$\mu$$时，为了检验估计的准确性，一般通过计算$$\hat{\mu}$$ 的标准误差standard error来衡量： $$Var(\hat{\mu})=SE(\hat{\mu})^2=\frac{\sigma^2}{n}$$ 。这里的SE是用来计算单一的样本均值估计值偏离真实值的情况，**SE随n的增大而减小**

同样也可以用SE来计算线性回归参数的偏差 $$SE(\hat{\beta_0})^2$$ 和$$SE(\hat{\beta_1})^2$$，所以区间$$[\hat{\beta_1}-SE(\hat{\beta_1})^2,\hat{\beta_1}+SE(\hat{\beta_1})^2]$$中有约95%的可能会包含 $$\beta_1$$ 的真实值，同理可知$$\beta_0$$的置信区间。

**SE功能2——对系数进行假设检验：**对于验证X和Y是否有线性关系，一般会引入假设检验，H0：X和Y之间没有关系，相当于检验 $$H_0:\beta_1=0$$。此时可以根据$$SE(\hat{\beta_1})^2$$来初步判定，如果$$SE(\hat{\beta_1})^2$$很小，那么即使$$\hat{\beta_1}$$比较小，$$\hat{\beta_1}$$的置信区间也在0之外，所以可以拒绝NULL假设。具体地说，进行对$$\hat{\beta_1}$$的均值进行t-test， $$t=\frac{\hat{\beta_1}-0}{SE(\hat{\beta_1})}$$，t-test具有钟型分布，当n&gt;30时，类似于正态分布。当p-value很小时，就拒绝NULL假设。

### 评价模型的准确性：

#### RSE\(Residual Standard Error\): 估计偏差 $$\epsilon$$ 

$$RSE=\sqrt{\frac{1}{n-2}RSS}=\sqrt{\frac{1}{n-2}\sum (y_i-\hat{y_i})^2}$$ ，RSE的意义为即使所有参数都是完全正确的，预测值离真实值仍存在RSE的偏差。但一般也用来估计模型的优劣，当RSE比较大时，说明模型离真实值也比较远。**Disadvantage:** RSE是以y作为参数的，即使计算出来也不知道怎么优化模型。

#### $$R^2$$统计量：

$$R^2=\frac{TSS-RSS}{TSS}=1-\frac{RSS}{TSS}=1-\frac{\sum (y_i-\hat{y_i})^2}{\sum (y_i-\bar{y_i})^2}$$，其中总平方和Total Sum of Square是$$TSS=\sum (y_i-\bar{y_i})^2$$ 。$$R^2\in(0,1)$$当接近1时说明回归可以解释相应变量的大部分变动，当接近0时说明回归模型和相应变量的关系不大，可能时因为模型是错误的，也可能是固有误差较大，或两者都有。

#### Correlation相关性：不能用在多元回归中

$$Cor(X,Y)=\frac{\sum (x_i-\bar{x})(y_i-\bar{y_i})}{\sqrt{\sum (x_i-\bar{x_i})^2}\sqrt{\sum (y_i-\bar{y_i})^2}}$$和$$R^2$$一样也衡量了X和Y的线性关系，事实上对于简单线性相关，$$R^2=r^2$$，但相关性并没有自动扩展到多元情境中，因为相关性只衡量一对变量之间的关系。 

## Multiple Regression

Slope in simple regression indicate the relationship between y and only single x and ignore other features , slopes in mutiple regression indicate the relationship between y and only single x and other features are still.

In a multiple regression, the coefficient before some variables may be very small, it seems useless to predict y, however, if make a correlation matrix among all variables and y, that variable may has strong relationship to other variables or y. 

Some simple regression may indicate ridiculous story, such like shark attack has positive correlation with sales of icecream. The fact is this regression is lack of the most important predictor, the temperature. High temperature causes more persons play at beach and bring better sales of icecream and count number of shark attack.

### Relationship between Y and Xs

#### Determine all variables

To determine whether there is a relationship between Y and all Xs, we can implement F-statistic. We create a null hypothesis $$H_0: \beta_1=\beta_2=...=\beta_p=0$$, then $$F=\frac{(TSS-RSS)/p}{RSS/(n-p-1)}$$. 

* $$H_0$$is true: If the null hypothesis is true, the value of F should be close to 1. Or if n is small, F should be large to reject $$H_0$$
* $$H_1$$is true: the value of F should be much greater than 1. Or if n is large, even F is a litter greater than 1, it should be fine

#### Determine subset of variables

### Choose important variables

* Akaike Information Criterion \(AIC\)
* Bayesian Information Criterion \(BIC\)
* Adjusted $$R^2$$ 
* Forward selection. From null model \(only contain $$\beta_0$$\), add one variable each time, and calculate the RSS. Find the minimum of RSS
* Backward Selection. From all variables, and **delete the greatest p-value** item each iteration until meet some criterion. But if p &gt; n, can't use Backward Selection.
* Mixed Selection. Mix forward and backward selection.

### Evaluation

Gernerally, RSE smaller and $$R^2$$greater, the model is better.

* RSE:$$RSE=\sqrt{\frac{1}{n-p-1}RSS}=\sqrt{\frac{1}{n-p-1}\sum (y_i-\hat{y_i})^2}$$
* $$R^2$$ : In multiple regression, the $$R^2=Cor(Y, \hat{Y})^2$$. We can measure the value of $$R^2$$, if delete or add a variable can cause this value change significantly, this variable should be important.

## Qualitative Prediction





