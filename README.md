## Overview
The data cleaning and exploratory data analysis are handled in the 3A notebook, the output of which is a cleaned master dataframe containing data for both subreddits. This master dataframe is read in and used in the 3B notebook, where several classifiers are built and test, and a final, best model is fit and tested on title and selftext data.

## Executive Summary
Our goal for this analysis is somewhat open-ended. At the center of it is the concept of Natural Language Processing (NLP), which in the context of machine learning, calls for a model to process and fit on large amounts of human language data in order to make relevant conclusions. In our case, we are setting out to create an NLP Classifier fit on two distinct pages from Reddit. Our goal will be to create a model capable of accurately predicting to which subreddit a given post belongs, based on the diction used in that post.

Our two chosen subreddits are r/PersonalFinance and r/Investing. These two pages share a number of similarities, particularly in their focus on financial concepts and money management, but they are naturally different in the scale and scope of discussions hosted. Investing generally tends to focus on public markets, firm decisions that affect markets and investment portfolios, etc. Personal Finance tends to host discussions more focused on individual financial questions and issues, with many related to things like taxes, savings accounts, career-related finances, etc.

By training our NLP classifier on the linguistic content on each subreddit, we hope to build a model capable of distinguising between r/Investing and r/PersonalFinance effectively enough to predict where a theoretical new post would be best suited.

## Data Dictionary
|Feature|Type|Description|
|---|---|---|
|**title**|*String*|Title of each post|
|**author**|*String*|Author username (not used)|
|**selftext**|*String*|Actual content of each post|
|**created_utc**|*String*|Epoch of creation of post (used only in EDA)|
|**subreddit**|*Binary*|0 is r/PersonalFinance, 1 is r/Investing|


## Conclusions

### Scale
Our analysis confirmed initial impressions that r/Investing tends to have discussions focusing on larger-scale financial concepts, including the stock market, large companies and their financial performance, as well as some macroeconomics and government spending. This is exemplified by some of the most influential words from this subreddit: 'Investor', 'Public', 'Fed', etc. 

On the Personal Finance side, we see financial concepts more related to individual or family finance, with discussions about account types, credit health, savings, career-related finances, etc. This is again exemplified by influential words on this side: 'budget','score','car','salari'.

### Overlap
Our most common instance of misclassification was that in which the best model misclassified a number of r/PersonalFinance posts as r/Investing. Upon some qualitative investigation, it seemed that the primary cause of this was the fact that many posts on r/PersonalFinance asked/opened discussion about investing, and these posts could justifiably have been posted on r/Investing. This put the model in a difficult position of being somewhat incapable of fully accounting for that "bleed-in," which likely also forced a cap on maximum accuracy.

It's worth noting that the best model, as well as all of those created, were based entirely on word and bigram counts, and did not truly account for sematic meaning. Using a different method of vectorization and possibly a neural network could potentially account for the sematic differences between average r/Investing posts and investing-related posts on r/Personal Finance.

### What are People Talking About?
As this analysis is by nature exploratory, it seems appropriate to pull out a couple of specific observations after modeling regarding the discourse occurring on each subreddit. 
#### Personal Finance: Tough Times
From both initial observations and insights from modeling, it becomes clear that a lot of members of r/PersonalFinance are seeking help with budgeting, and oftentimes because they are managing with limited resources. Many have been laid off or furloughed due to the COVID-19 pandemic, and are struggling to manage finances as a result of these circumstances. 
#### Investing: Tesla 
One interesting insight from our best model's word coefficients was that 'Tesla' seemed to be an important influencer for the likelihood that a prediction was r/Investing. Upon some investigation on the subreddit and a bit of outside research, my hypothesis for the reasoning behind this is the fact that Tesla has had a significant reversal in financial performance since 2019, which has significantly influenced investor interests and has likely brought in a lot of new investors. Despite somewhat slow performance in the U.S. during the pandemic, they've managed to maintain a stronger market in China that has boosted their stock price throughout most of 2020.