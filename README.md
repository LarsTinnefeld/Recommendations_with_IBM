# Recommendations of IBM Watson Articles
Recommendations with Collaborative Filtering and Matrix Factorization (SVD)

Lars Tinnefeld
2021-02-20

![Recommendation](https://cdn.pixabay.com/photo/2018/03/19/13/43/feedback-3240007_960_720.jpg)

*Image: [mohamed_hassan](https://pixabay.com/users/mohamed_hassan-5229782/) on Pixabay

## Table of content
1. [Introduction](#business_understanding)
2. [Objectives](#objectives)
3. [Data](#data)
4. [Data preparation](#preparation)
5. [Data Modelling](#modelling)
6. [Evaluation](#evaluation)

## Inroduction <a name="business_understanding"></a>
This project is part of Udacity's Data Science Nanodegree program and was provided by IBM Watson Studio. IBM Watson Studio is managing a platform which provides articles to their user community. Selected articles are presented to users on the landing page's dashboard. Users can react to the content by communicating via email. These interactions are the only way a user's interest could be measured. The provided datasets contain the anonymized email adresses along with the article-ID the message was dealing with and a lookup table in which the articles are listed with their ID and content.

## Objectives <a name="objectives"></a>
IBM is asking in this project to investigate ways to develop an algorithm which can recommend articles to users on the dashboard. The selection of these articles should be based on the recommendation algorithm. The objectives can be broken down to sub-tasks in the following way:

- Exploratory Data Analysis
- Rank-Based Recommendations
- User-Based Collaborative Filtering
- Content-Based Recommendations
- Matrix Factorization

## Data <a name="data"></a>
`articles_community.csv`: Lookup table which contains all articles

| # |  Column | Non-Null Count | Dtype | Content |
| --- | --- | --- | --- | --- |
| 0 | doc_body | 1042 non-null | object | Full text content |
| 1 | doc_description | 1053 non-null | object | Summary of content |
| 2 | doc_full_name | 1056 non-null | object | Name of article |
| 3 | doc_status | 1056 non-null | object | Flag if document is live |
| 4 | article_id | 1056 non-null | int64 | ID of the article |

`user-item-interactions.csv`: Data table which contains all user-article interactions

| # |  Column | Non-Null Count | Dtype | Content |
| --- | --- | --- | --- | --- |
| 0 | article_id | 45993 non-null | float64 | ID of article |
| 1 | title | 45993 non-null | object | Name of article |
| 2 | email | 45976 non-null | object | Anonymized email address |

## Data preparation <a name="preparation"></a>
The data preparation is consisting of data wrangling and Exploratory Data Analysis.

Data wrangling:
- Searching for missing valus
- Dealing with duplicates

EDA:
- Count of unique users
- Count of unique articles in both datasets
- Distribution of interactions
- Count of unique user-article interactions

![dist](https://github.com/LarsTinnefeld/Recommendations_with_IBM/blob/main/Interact_dist.png?raw=true)

## Data modelling <a name="modelling"></a>
1) Rank-based recommendations
2) User-User-based collaborative filtering
3) Content-based recommendations
4) Matrix factorization (SCD)

## Evaluation <a name="evaluation"></a>

![err1](https://github.com/LarsTinnefeld/Recommendations_with_IBM/blob/main/Error_dev_1.png?raw=true)

![err2](https://github.com/LarsTinnefeld/Recommendations_with_IBM/blob/main/Error_dev_2.png?raw=true)

**Observations**

In the last analysis (step 5) the accuracy drops with increasing number of latent features. This is the opposite effect of what we have seen in the excercise with the total dataset. Interestingly, the accuracy flattens at round about 0.964.
The effect caused by changing the number of latent feature is very little when we compare the accuracy scale. We could do a statistical hypotheses test to see if the effect is even sufficient to be significant enough to be counted as valid.
The small number of only 20 users in the last dataset is most likely not a good sample size to represent the total population.
There is a significant imbalance between the 1s and the 0s. This might be the reason why the accuracy is not dropping below 0.964 and not further, and is therefore always in a very high range.
Considerations to measure the effects of one of the above recommendation methods

In order to measure the effect of the recommendation methods we will need to implement a better statistical base. A good test would rely on a few conditions:

Evaluation of the imbalance. Taking action if the imbalance is exceeding the acceptable range by trying to counter the effect with upsampling, downsampling, AUROC etc.
Evaluation of the sample size. 20 users is not be a good representation for the total population of over 5000. Use statistical evaluation methods which deal with such small samples (Student t-test etc.)
We could try to develop the above proposed content-based recommendation by analyzing the article body. This would include an NLP alorithm which breaks down the text into words, tokenize these words and remove stop words. The feature (list of words) could then be the base to find similarity between the articles and therefore could predict shared interest between users.
Investigation if not other, not considered, conditions led to a higher interaction rate of specific articles. For example: articles on top of a list will have in general more attention then the ones at the bottom, and therefore will have naturally more interaction.
Suggested process towards a good evaluation and eventually a good recommendation algorithm

To get to a good test evaluation and eventually a well performing recommendation algorithm, there will need to be a few actions to be implemented. Below is a proposed process to be reviewed and evaluated regarding feasibility. The final procedure would be a A/B test which is based on good evaluation metrics. The process would include:

Expand the view on the user interaction to a funnel instead of a single interaction metric "1/0". This would include to capture homepage visit, scrolling, clicking and more.
Defining better evaluation metrics. The above suggested funnel would introduce new cookie based features. In addition to that a simple rating method (arrow up/ arrow down) would not overcomplicate the user interaction and introduce a good new metric for evaluation.
The invariant metric needs to be taken into account. The user groups would need to be sized according statistical aspects: random, balanced
Experiment sizing: The time period for the test must be suffitient to exceed the statictically significant threshold. This means that the experiment must run long enough to collect enough data to be a valid sample size. Valid in this context means to contain a low enough probability for a Type I error.
Eventually, we also would need to be aware that the new process would need to be not just better, but improve enough to justify the effort to implement it. The KPIs to capture this needs to be defined. Along with this, new aspect of ethic need to be considered. New data about users will need to be in line with regulations and transparency towards the users.
