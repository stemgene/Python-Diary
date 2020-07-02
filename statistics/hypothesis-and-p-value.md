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

Type I Error $$\alpha$$ : False Positive. 二者其实没有区别，结果落在了$$\alpha$$区间内，即本来不应该选，但选中了。反映到日常案例中就是网页改动没有效果，但是错误的判断有效果。

Type II Error $$\beta$$: False Negative，二者本来有区别，因为选择的margin是t\*，当测试集中的数据处于t\*左侧，即$$\beta$$区域，所以错误的认为没有区别。反映到日常案例中就是实验结果好（网页改动有比较显著的效果），但判断时认为改动没有效果。

Power: the probability of rejecting H0 when it is, in fact, wrong。 $$Power=1-\beta$$ 

![](../.gitbook/assets/image%20%2871%29.png)

## A/B Testing

主要应用在比较成熟的产品上，对产品有有限的几处改动，而且满足可以测试的人比较多的情况。

* A是原来的产品功能control group，B是新的产品功能实验组experiment group。
* 需要确定关注指标如click through ratio是不是提升

### Steps:

1. Customer Funnel. Funnel analysis for each customer steps
2. **Define Metrics. Click-through rate, convert rate, bounce rate**
3. **Hypothesis.**
4. Formulate test plan. Make a plan to define 'good'
5. **Create Variation. compares a variation against current**
6. **Run Experiment. Choose significance level, sample size**
7. **Analyze test result. Sanity check, metrics evaluation**
8. Conclusion

