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

## Data modelling <a name="modelling"></a>
1) Rank-based recommendations
2) User-User-based collaborative filtering
3) Content-based recommendations
4) Matrix factorization (SCD)

## Evaluation <a name="evaluation"></a>
