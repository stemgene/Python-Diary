# Hypothesis



## Steps of Hypothesis:

1. Design Hypothesis, H0 and H1.
2. Determine which test to be used? Z-test, t-test, F-test
3. Compute test score, one tail or two tails
4. P-value, alpha
5. Theoretical conclusion

## **P-value**

When we execute a **hypothesis test** in statistics, P-value is used to **determine the significance** of results after a hypothesis test in statistics. The definition of P-value is: The probability of observed or more extreme outcome, given that the null hypothesis is true. Null Hypothesis: no effects or no difference

P-value helps the readers to draw conclusions and is always between 0 and 1.

* P- Value &gt; alpha \(e.g., 0.05\) denotes weak evidence against the null hypothesis which means the null hypothesis cannot be rejected. it is likely to observe the data even if the null hypothesis is true
* P-value &lt;=  alpha\(e.g., 0.05\) denotes strong evidence against the null hypothesis which means the null hypothesis can be rejected, it is very unlikely to observe the data if the null hypothesis is true

### Type I & II Error, Power

**Type I Error** $$\alpha$$ : False Positive. $$\alpha=P(reject H_0 | H_0 is ture)$$ 二者其实没有区别，结果落在了$$\alpha$$区间内，即本来不应该选，但选中了。反映到日常案例中就是网页改动没有效果，但是错误的判断有效果。

**Type II Error** $$\beta$$: False Negative，$$\beta=P(accept H_0 | H_0 is false)$$二者本来有区别，因为选择的margin是t\*，当测试集中的数据处于t\*左侧，即$$\beta$$区域，所以错误的认为没有区别。反映到日常案例中就是实验结果好（网页改动有比较显著的效果），但判断时认为改动没有效果。

样本的多少决定了分布跨度的大小，当样本越多，分布越收敛，尾部的概率就越小。

**Power:**  $$Power=1-\beta=P(reject H_0 | H_0 is false)$$, should &gt; 0.8

三者关系： $$\alpha$$⬆ $$\beta$$⬇ Power⬆

![](../.gitbook/assets/image%20%2871%29.png)

## Confidence Interval vs Hypothesis

Sample mean的置信区间和Hypothesis有着数学上的关系。对于一个双边z-test，阴影部分叫**rejection region**，任何落在\[-1.96, 1.96\]之间的z值所反映的是p-value &gt; 0.05，接受H0。-1.96和1.96称作**critical values**。

![](../.gitbook/assets/image%20%2876%29.png)

* Confidence interval：根据sample mean给出总体 $$\mu$$ 一个合理的区间。求出critical value $$Z_{\alpha}=qnorm(\alpha)$$，接着再比较 $$|Z|$$ 和 $$Z_{\alpha}$$ 的关系 
* Hypothesis: 根据p-value来决定是否预估的值是正确的，收集证据去拒绝H0。由 $$Z=\frac{\bar{x}-\mu_0}{\sigma/\sqrt{n}}$$求Z，然后P=norm\(Z\) ，判断P与 $$\alpha$$ 。

## 各种检验方法

![](../.gitbook/assets/image%20%2872%29.png)

### Z-test

### t-test

#### 单个样本组的t-test

![](../.gitbook/assets/image%20%2875%29.png)

$$t=\frac{\bar{x}-\mu_0}{s/\sqrt{n}}$$，df=n-1 

#### 比较两组数据的t-test：首先决定这两组population是paired还是独立的

![](../.gitbook/assets/image%20%2874%29.png)

**1.Paired Samples: 同一群体不同时间，有相同均值的**

| **Before** | After | d=Difference |
| :--- | :--- | :--- |
| 55 | 60 | -5 |
| 62 | 75 | -13 |
| 61 | 65 | -4 |
| 72 | 89 | -17 |

$$H_0:\mu_d=0$$； $$H_1:\mu_d\ne0$$，只对difference感兴趣。

$$\bar{X_d}=\frac{\sum{d}}{n}$$ ， $$s_d=\sqrt{\frac{\sum{(d_i-\bar{x})^2}}{n-1}}$$，stand error \(SE\) = $$\frac{s_d}{\sqrt{n}}$$ 

**2. Independent Samples:** $$\mu_1$$和$$\mu_2$$是不同的，每组有自己的n，$$\mu$$ 和 $$\sigma^2$$ ，且都是normal distribution。

1. Variance equal: $$\sigma^2_1=\sigma^2_2$$ 

![](../.gitbook/assets/image%20%2873%29.png)

* $$\sigma^2$$is known, Z-test. $$SE=\sqrt{\sigma^2(\frac{1}{n_1}+\frac{1}{n_2})}$$， $$Z=\frac{(X^2_1-X^2_2)-(\mu_1-\mu_2)}{SE}=\frac{(X^2_1-X^2_2)-(\mu_1-\mu_2)}{\sqrt{\sigma^2(\frac{1}{n_1}+\frac{1}{n_2})}}$$ 
* $$\sigma^2$$is unknown, t-test. 用 $$S^2_p=\frac{(n_1-1)S^2_1+(n_2-1)S^2_2}{n_1+n_2-2}$$替换$$\sigma^2$$

  $$t=\frac{(\bar{X^2_1}-\bar{X^2_2})-(\mu_1-\mu_2)}{\sqrt{S^2_p(\frac{1}{n_1}+\frac{1}{n_2})}}$$, df=n-2

以上方法是计算p-value的，也可以通过计算置信区间，用 $$t_{\frac{\alpha}{2}}=qt(1-\frac{\alpha}{2}, df)$$，然后再 $$(\bar{X_1}-\bar{X_2})\pm t_{\frac{\alpha}{2}}\sqrt{S^2_p(\frac{1}{n_1}+\frac{1}{n_2})}$$查看置信区间的范围。

     2. Variance unequal \(Welch t-test\):$$\sigma^2_1\ne\sigma^2_2$$

![](../.gitbook/assets/image%20%2877%29.png)

此时$$(\bar{X_1}-\bar{X_2})\sim N(\mu_1-\mu_2,\sqrt{\frac{s_1^2}{n_1}+\frac{s_2^2}{n_2}})$$， $$t=\frac{(\bar{X_1}-\bar{X_2})-(\mu_1-\mu_2)}{\sqrt{\frac{s_1^2}{n_1}+\frac{s_2^2}{n_2}}}$$ 

### F-test \(Inference for variances\)

### Inference on Proportions \(Binary variable\)

#### 通过Confidence Intervals推断事件发生的概率

Example: 62人中有53人是右手，推断right-hand proportion

Step 1： $$\hat{p}=\frac{X}{n}=\frac{53}{62}$$， $$\hat{p}$$是point estimate of p。当 $$np\ge5$$ and $$n(1-p)\ge5$$时， $$\hat{p}\sim N(p, sd=\sqrt{\frac{p(1-p)}{n}})$$ 

Step 2: $$Z= \frac{\hat{p}-p}{\sqrt{\frac{p(1-p)}{n}}}$$, 所以包含true p的置信区间就为

* two-sides: $$(\hat{p}-Z_{\frac{\alpha}{2}}\sqrt{\frac{\hat{p}(1-\hat{p})}{n}}, \hat{p}+Z_{\frac{\alpha}{2}}\sqrt{\frac{\hat{p}(1-\hat{p})}{n}})$$，且当 $$\alpha=0.95$$时， $$Z_{\frac{\alpha}{2}}=1.96$$ 
* one-side lower: $$(\hat{p}-Z_{\frac{\alpha}{2}}\sqrt{\frac{\hat{p}(1-\hat{p})}{n}}, 1)$$
* one-side upper: $$(0, \hat{p}+Z_{\frac{\alpha}{2}}\sqrt{\frac{\hat{p}(1-\hat{p})}{n}})$$

for our example, $$\hat{p}=\frac{53}{62}=0.855$$, for 95% confidence interval, we have$$0.855\pm1.96\sqrt{\frac{0.855(1-0.855)}{62}}=(0.767, 0.943)$$

#### 估计样本size

#### 比较两组数据的proportion

Example: 比较男性和女性右手的比例是否一致

 

## A/B Testing

主要应用在比较成熟的产品上，对产品有有限的几处改动，而且满足可以测试的人比较多的情况。

* A是原来的产品功能control group，B是新的产品功能实验组experiment group。
* 需要确定关注指标如click through ratio是不是提升
* 在实验中会遇到Type I or II的情况，此时可以提高样本量或者延长实验时间，会使两个分布更分开一些。

### Steps:

1. Customer Funnel. Funnel analysis for each customer steps
2. **Define Metrics. Click-through rate, convert rate, bounce rate**
3. **Hypothesis.**
4. Formulate test plan. Make a plan to define 'good'
5. **Create Variation. compares a variation against current**
6. **Run Experiment. Choose significance level, sample size**
7. **Analyze test result. Sanity check, metrics evaluation**
8. Conclusion

