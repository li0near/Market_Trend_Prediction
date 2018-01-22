# Market-Trend-Prediction

This is a course project of Building Knowledge Graph. The goal of this project is to predict the trend of the Dow Jones Industrial Average (DJIA) based on the integration of historical stock prices of the 30 component companies of DJIA and general opinions towards them extracted from social media posts and news reports.

## Approach

### Data Collection

1. **Sturctured data**: leveraging official APIs to crawl historical stock price data from Yahoo Finance and posts from Facebook and Twitter.
2. **Unstructured data**: using [ACHE](https://github.com/ViDA-NYU/ache) to scrape Business Insider articles and Reddit financial threads.
3. Product golssary: the names of products of each company were collected from [DBpedia](http://wiki.dbpedia.org), [Wikipedia](https://www.wikipedia.org) and their official websites. The glossary may not be exhaustive but was sufficient enough for the project purpose.

Data collecting range: Aug 1, 2016 to Nov 30, 2017.
Training data range: Aug 1, 2016 to Oct 31, 2017.
Number of records: Business Insider (2,017), Reddit Finance (4,383), Facebook (11,528), Yahoo Finance(10,478), Twitter (24,271).

### Data Manipulation

1. Data cleaning: filter out only the content, namely articles, posts and web pages, relating to the DJIA 30 component companies. This is done by fuzzy string matching company names and their corresponding product names with text from each post or web page.
2. Information extraction: utilize NLP to determine the opinion polarities of articles and posts, followed by properly tagging along with the corresponding company name.
3. Data integration: combine and organize data from different sources into one CSV file for Machine Learning, and another several JSON Lines files for generating knowledge graph in [myDIG](https://github.com/usc-isi-i2/dig-etl-engine).

### Predict Results
1. Please refer to [this link](https://github.com/Cheng-Lin-Li/Market-Trend-Prediction/blob/master/source/Dow%20Jones%20Industrial%20Average%20Prediction%20with%20Media%20Channel%20Info-with%20Social%20Info.ipynb) for the Jupyter code of prediction results with social media information as part of the input features.

2. Please refer to [this link](https://github.com/Cheng-Lin-Li/Market-Trend-Prediction/blob/master/source/Dow%20Jones%20Industrial%20Average%20Prediction%20without%20Social%20media%20data.ipynb) for the Jupyter code of prediction results without including social media features.

```text
                Next-day Prediction

              precision    recall  f1-score   support

Decrease       0.00      0.00      0.00         7
Increase       0.70      1.00      0.82        16

avg / total    0.48      0.70      0.57        23

               Next-month Prediction

              precision    recall  f1-score   support

Increase       1.00      1.00      1.00        23

avg / total    1.00      1.00      1.00        23 
```

### Program list

|Program|Description|Link|
|------|------|--------|
|[JSONLines](https://github.com/Cheng-Lin-Li/KnowledgeGraph/tree/master/CDR_JSONLines)|Json Lines aggregate all of the crawled web pages into a single file, each line of which is a single JSON object representing one page.| [Source Code](https://github.com/Cheng-Lin-Li/KnowledgeGraph/blob/master/CDR_JSONLines/jsonlines.py)|

|[JSONLines content classifier program](https://github.com/Cheng-Lin-Li/Market-Trend-Prediction/blob/master/source/classify.py)|The input is a json line document and a new json line file containing only the pages relevant to dow 30 companies based on glossary of Dow30 companies and their products. New tags containing company and product names will be added to html body to make it convenient for inferlink. NLTK tools was used for positive, negative message or post recognition. rltk tools was adopted to perform string similarity for web content and glossary of company names and productions.|[Source Code](https://github.com/Cheng-Lin-Li/Market-Trend-Prediction/blob/master/source/classify.py)|

|[Data Integration program](https://github.com/Cheng-Lin-Li/Market-Trend-Prediction/blob/master/source/dataintegration.py)| This program based on csv file of Dow30 companies and add with facebook, twitter social media likes, dislikes into csv for machine learning input. |[Source Code](https://github.com/Cheng-Lin-Li/Market-Trend-Prediction/blob/master/source/dataintegration.py)|

|[Facebook Crawler for Dow30](https://github.com/Cheng-Lin-Li/Market-Trend-Prediction/blob/master/source/facebook-crawler-dow30.py)| This is a crawler program to crawl facebook post via facebook graph api. A special facebook id and Dow 30 companies dictionary are integrated into this version. A CSV with like, dislike will provide by this program for machine learning. |[Source Code](https://github.com/Cheng-Lin-Li/Market-Trend-Prediction/blob/master/source/facebook-crawler-dow30.py)|

|[Yahoo Crawler for Dow30](https://github.com/Cheng-Lin-Li/Market-Trend-Prediction/blob/master/source/yahoo_quote_crawler.py)| This is a crawler program to crawl yahoo finance stock price via yahoo api. A special ticker id and Dow 30 companies dictionary are integrated into this version. A CSV with full company name will provide by this program for machine learning purpose. Input a list of stock ticker and time period for those price data. |[Source Code](https://github.com/Cheng-Lin-Li/Market-Trend-Prediction/blob/master/source/yahoo_quote_crawler.py)|

|[Twitter Crawler for Dow30 Companies](https://github.com/Cheng-Lin-Li/Market-Trend-Prediction/blob/master/source/tweetScraper.py)| This program scrapes the offcial Titter accounts of Dow components |[Source Code](https://github.com/Cheng-Lin-Li/Market-Trend-Prediction/blob/master/source/tweetScraper.py)|

### Team members

[Cheng-Lin Li](https://github.com/Cheng-Lin-Li/) & [YuCheng Guo](https://github.com/li0near)

### Date: Project kick off date

Oct., 2017@University of Southern California

## Contact Information

Cheng-Lin Li: chenglil@usc.edu
Yucheng Guo: yuchengg@usc.edu
