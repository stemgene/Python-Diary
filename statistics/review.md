# Review

## Classical Categories:

![](../.gitbook/assets/image.png)

* Regression:
  * Linear: Wage ~ age, education level
  * Non-linear
* Classification:
* Clustering: 基因表达

## Prediction & Inference

* Prediction: $$\hat{Y}=\hat{f}(X)+\epsilon$$ ，由X推导$$\hat{Y}$$，不太关注$$\hat{f}$$具体的内容
* Inference：研究$$\hat{Y}和\hat{f}(X)$$的关系，如Y和X是否相关？哪个X对Y的影响更大？改变哪个X可以改变Y

## Estimate $$\hat{f}$$

* 参数法，如 $$f(X)=\beta_0+\beta_1X_1+\beta_2X_2+...+\beta_pX_p$$ 
  * Advantage: 由于预估出参数模型，用较少的训练样本可以拟合函数 $$f(X)$$ 
  * Disadvantage: 很多情况下，无法用参数和变量之间的关系来表达出具体的函数形式，或者估计的 $$f$$ 形式与真实的存在较大差异。
* 非参数法，不需要事先估计$$f$$的形式
  * Advantage: Don't need to know $$f$$
  * Disadvantage: need more data

