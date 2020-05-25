# Latent factor model隐语义模型

除了UserCF和ItemCF之外，还有为物品自身分类的算法，其中Latent factor model采取基于用户行为统计的自动聚类，为物品分类。除了隐性数据之外，LFM在线性反馈数据（评分数据）上解决评分预测问题也有很好的精度。

## 基本算法

LFM用于计算用户u对物品i的兴趣，$$Preference(u,i)=r_{ui}=p^T_uq_i=\sum_{f=1}^{F}{p_{u,k}q_{i,k}}$$，其中 $$p_{u,k}$$和 $$q_{i,k}$$是模型的参数，$$p_{u,k}$$ 度量了用户u的兴趣和第k个隐类的关系，而$$q_{i,k}$$度量了第k个隐类和物品i之间的关系。这两个参数需要通过training set学习出来，对于每个用户u，training set中都包含了用户u喜欢的物品和不感兴趣的物品，通过training获得模型参数。

隐形反馈数据集只有正样本（用户喜欢什么物品），而没有负样本（用户对什么物品不感兴趣）。在此数据集上应用LFM解决TopN推荐的第一个关键问题就是给每个用户生成负样本。原则是对于一个用户，从他没有过行为的物品中采样出一些物品作为负样本，但采样时保证每个用户的正负样本数目近似，而且要选取那些很热门，而用户却没有行为的物品。因为很热门但用户没有行为更加代表用户对这个物品不感兴趣。

通过code按照物品的流行度采样出热门的但用户却没有过行为的物品后，得到一个用户--物品集K={\(u, i\)}，其中如果\(u, i\)是正样本，则有 $$r_{ui}=1$$，否则$$r_{ui}=0$$（比如网站首页推送的链接，用户u点击，就是$$r_{ui}=1$$，反之$$r_{ui}=0$$）。然后需要优化如下的loss function来找到最合适的参数p和q：

![](../.gitbook/assets/image%20%2860%29.png)

$$\lambda||p_u||^2+\lambda||q_i||^2$$是用来防止过拟合的正则化项，用梯度下降来最小化loss function。首先对参数p和q求偏导 $$\frac{\partial C}{\partial P_{uk}}=-2q_{ik}+2\lambda p_{uk}$$和 $$\frac{\partial C}{\partial q_{ik}}=-2p_{uk}+2\lambda q_{ik}$$。然后梯度下降，将参数沿着最快度下降方向推进，得到递推公式： $$p_{uk}=p_{uk}+\alpha(q_{ik}-\lambda p_{uk})$$ 和 $$q_{ik}=q_{ik}+\alpha(p_{uk}-\lambda q_{ik})$$ ，alpha是learning rate。

经验参数：

* 负样本/正样本比例ratio。对LFM的性能影响最大，需要固定下面3个参数单独研究此项
* Latent factor个数F：F=100
* alpha=0.02
* lambda=0.01

## 性能评测

用LFM计算出兴趣向量p和物品向量q之后，对于每个隐类找出权重最大的物品（$$q_{ik}$$最大）

![](../.gitbook/assets/image%20%2842%29.png)

随着负样本数目的增加，LFM的precision和recall有明显提高，不过当ratio&gt;10之后，准确率就比较稳定了。同时随着负样本数目增加，coverage不断降低，流行度不断增加，说明ratio参数控制了发掘长尾的能力。如果和[UserCF及ItemCF算法](https://app.gitbook.com/@hlj12530/s/stemgene/~/drafts/-M883h1WhOKQlQH6SIcj/recommendation-system/neighborhood-based)的性能相比，LFM在所有指标上都优于它们。

LFM模型的困难：因为每次训练时都需要扫描所有的用户行为记录，很难实现实时推荐。

|  | LFM | 邻域方法 |
| :--- | :--- | :--- |
| 理论基础 | 学习方法，比较好的理论基础 | 基于统计的方法 |
| 复杂度 | 很节约空间，时间上没有区别 | 空间是M平方 |
| 能否实时推荐 | 很难，用户有了新的行为后，推荐列表不会变化 | 可以 |
| 解释性 | 无法解释 | ItemCF可以 |

