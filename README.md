# Yelp Review Analysis

## Project Background 
Nowadays, people can recommend a restaurant to others simply by writing a review on Yelp. They can write anything about a restaurant, including parking, location, services, environment and food. For foodies, they can use these reviews as references to decide if they want to try a restaurant or not. Also, for restaurant owners, they could use these reviews to evaluate the performance of their restaurants. They could identify their popular dishes, improve their services or change their layouts accordingly. 

## Project Overview
We performed text analytics on yelp dataset to derive business insights from customers’ restaurant reviews. We summarized recent restaurant performances from restaurant reviews, generated polarity scores of individual restaurants through sentiment analysis, and extracted main topics through Topic Modeling on AWS(S3,EC2,EMR), PySpark and Python. We also developed and presented a dashboard for business owners on Tableau. We hope these insights could help restaurants better serve their customers. 

![](Photos/business_flow.png)

## Technical Architecture
The data was downloaded from [Yelp Open Dataset](https://www.yelp.com/dataset) in JSON format. The dataset contains 192,609 businesss and 6,685,900 reviews. Due to the large scale of the dataset, we performed our analysis using Amazon Web Services(AWS) and Pyspark. To be specific, we used Amazon S3 for data storage, Amazon EC2 and EMR for cloud computing and transformation. We also used Pyspark on Databricks for sentiment analysis and predictive modeling. We used Python for building LDA models and Tableau for creating dashboards. 

![](Photos/data_flow.png)

## Project Walkthrough
The analysis consists 3 parts: 

- Exploratory analysis on the overall review trends across time
- Predictive modeling to identify misclassified reviews and calculate the polarity score based on sentiment analysis 
- Latent Dirichlet Allocation (LDA) model to determine key topics among reviews in negative and positive sentiments

### 1. Exploratory data analysis (EDA): 
We created visualizations for: 
- Average ratings of each resturant
- Total number of reviews for each rating
- Total number of reviews each month/year

### 2. Sentiment Analysis and Predictive Modeling

There is a misconception between rating score and customer satisfaction. High rating score may not imply high satisfaction (Eg: a 4-star rating may include negative comments since this customer thinks there’s improvement to be made). Therefore, we use sentiment analysis to quantify opinion (by generating polarity scores) solely based on texts. We built a linear regression model to identify comments that are in align with their ratings. Then we used these comments as the training data to build a SVM model. The model will predict whether the reviews are misclassified or not. The model is built in Pyspark, and the code can be found [here](https://github.com/peterwei425/Yelp-Review-Analysis/blob/master/SVM_sentiment.ipynb). 

### 3. Latent Dirichlet Allocation(LDA)/ Topic Modeling:  

After we identified positive and negative sentiments, we would like to further explore what specific messages they conveyed. For example, among all negative reviews, what aspects of restaurants do they talk about the most? Do they complain about food, services or environments?

To solve this problem, we used topic modeling to identify key messages or topics customers are talking about. We determine number of topics based on coherence score, which measures score a single topic by measuring the degree of semantic similarity between high scoring words in the topic. Then we identified the topic based on the word distribution of the topic. 

![](Photos/topic_model.png)

The LDA model was built in Python using [gensim](https://pypi.org/project/gensim/), and LDA visualizations was built with [pyLDAvis](https://pypi.org/project/pyLDAvis/). The code which extracted topics for 3 resturants in Las Vegas can be found [here](https://github.com/peterwei425/Yelp-Review-Analysis/blob/master/LDA.ipynb). 

## Dashboarding

We created a dashboard to summarize our analysis result and showcase to fellow students and analytic professionals. Our dashboard contains 3 parts: 

- Review Across Time
- Customer Satisfaction from Text Review
- Key Messages from Text Review

Here is a screenshot of the dashboard: 

![](Photos/dashboard.png)

We also published our dashboard in Tableau Public, which can be accessed [here](https://public.tableau.com/profile/xiangke.chen#!/vizhome/YelpReviewAnalysis_15758570841320/final). 

Team: [Boyang Wei](https://www.linkedin.com/in/boyang-wei/), [Yili Yu](https://www.linkedin.com/in/yili-yu-173b62179/), [Elizabeth Zhu](https://www.linkedin.com/in/elizabethyizhu/), [Shaco Chen](https://www.linkedin.com/in/xiangke-chen/), [Yusha Wang](https://www.linkedin.com/in/yusha-wang-analytics/), [Lin Xu](https://www.linkedin.com/in/lin-xu-8182ab15a/). 
