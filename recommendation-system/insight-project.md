# Insight project

## A recommendation mechanism for YouTuber

Youtube has a complex and perfect [recommendation system](https://research.google/pubs/pub45530/) for users. Videos will be push to users according to their historical records, the popularity of videos, and the new episodes of subscribed YouTubers. However, Youtube doesn't provide this mechanism to YouTubers and tell them which video does users like. As YouTubers, they may only rely on their intuition and interest.

### Structure of project

This project is divided into two parts, data collection part and recommendation algorithm part. The input of a recommendation system mainly consists of two parameters: user and item, those are the output of data collection & preprocessing part.

#### Data Collection:

| Youtube  | Category: Food, 12 months |
| :--- | :--- |
| video | category\_id/video\_id + title/ channel title/ time/views/\(dis\)likes/comment |
| channel\_id | comment\_text + likes/ historical video\_id + title |
| subscriber\[optional\] | id/likes AND food videos |
| Google trending\[optional\] | food name |

#### Data Preprocessing:

* NLP: pair title/comments with Food Corpus, and filter the key words of foods
* Assemble weights on subs

## Data

[python - youtube数据API评论分页](https://www.coder.work/article/1280254)

[YouTube Data in Python](https://medium.com/greyatom/youtube-data-in-python-6147160c5833)

[YouTube视频榜单SQL/Python/Excel数据分析](https://juejin.im/post/5e68984c518825495e105ea0#heading-14)

[Trending YouTube Video Statistics](https://www.kaggle.com/datasnaek/youtube-new/kernels)

## NLP

[NLTK学习之一：简单文本分析](https://blog.csdn.net/zzulp/article/details/77150129)

fuzzywuzzy模糊匹配

TF-IDF提取热词

[food语料库](https://www.researchgate.net/publication/337030736_FoodBase_corpus_a_new_resource_of_annotated_food_entities)

#### [快速生成食物向量](https://medium.com/shidanqing/%E5%BF%AB%E9%80%9F%E7%94%9F%E6%88%90%E9%A3%9F%E7%89%A9%E5%90%91%E9%87%8F-5cc39adfb291)

## Recommendation algorithm

{% embed url="https://blog.csdn.net/John\_xyz/article/details/78915150" %}

#### [推荐系统遇上深度学习\(二十五\)--当知识图谱遇上个性化推荐](https://zhuanlan.zhihu.com/p/48601941)

#### [近期必读的12篇「推荐系统」相关论文](https://www.ctolib.com/topics-138700.html)

