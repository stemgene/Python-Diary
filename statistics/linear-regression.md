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

