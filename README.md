# Problem Statement 

To combat misinformation Reddit would like to label submissions of  news articles as either fake news or real new based on the text in the post. This would increase user trust on the site and ultimately profits. We will use r/theonion and r/nottheonion subreddits as proxies to test if it is possible to get accurate classifications before employing the system site wide. 


# The Data 

- Gathered using PushShift Reddit API 
- 18451 posts from August 2,2021 -  May 21, 2013 
    - 8486 submissions from r/theonion  - 55%
    - 9965 from r/nottheonion - 45% 

- About 30 posts per month 
- Our goal is to be able to label posts based on the text in the submission so we will be focusing on title of each post 

**READER WARNING**: The information gathered was done so without filtering for explicit or offensive material in an effort to model based on real world data since content on reddit is not censored by default. The data gathered has observations containing explicit or otherwise offensive text.  


# Methodology

## Data Cleaning 
0. Combine data from both subreddits into one dataframe for further analysis 
1. Drop duplicate entries obtained during the data gathering process
2. Check for anomalies, such as posts by moderators, in each subreddit that do not fit the pattern of the other posts 
3. Remove URLs from the title to avoid classifying posts based on the link instead of the text content 
4. Remove posts without any text in the title as these will not provide any information for our purposes
5. Consider other features of the data 

## Modeling 
1. Make a baseline, equivalent to guessing at random, for comparison to production models 
2. Make multinomial naive bayes model with default hyperparamters 
3. Adjust relevant hyperparameters to optimize for metrics of value 
4. Make a decision tree model with default hyperparameters 
5. Adjust relevant hyperparameters to optimize for metrics of value 


# Conclusion and Recommendations

For the production multinomial naive bayes model there was a 38% increase in accuracy compared to the baseline model of guessing at random. For the production decision tree model there was a 32% increase in accuracy compared to the baseline model of guessing at random. 


The significant improvement from the baseline model in both the naive bayes and decision tree model suggests that it is possible to label submissions as “fake news” or “real news” based on the title.


It is recommended to train the classification model on more subreddits before deploying the feature across all of reddit to ensure it generalizes well. 

It is recommended to test other classification models like random forest to see if better accuracy can be achieved. 

Limitations of current model: 
- Not a lot data cleaning was performed so it may be possible to get better features after cleaning the data further  
- Basic transformer was used to vectorize text. By using a more complex transformer, such as TFIDF, that retains more of the context in the text it may be possible to get better results.  
- The model was only trained on two subreddits so the models ability to generalize to other subreddits may be limited. 
-  Only text from title of post was used for this model so it is likely that by adding other important features and metadata the model will perform better 


# Sources 

This study referenced the following sources: 

1. https://www.niemanlab.org/2019/01/a-typical-big-news-story-in-2018-lasted-about-7-days-until-we-moved-on-to-the-next-crisis/

2. https://github.com/pushshift/api 

3. https://regex101.com/

4. https://www.reddit.com/r/nottheonion/wiki/expanded

5. https://www.reddit.com/r/TheOnion/ 

6. https://stackoverflow.com/questions/11331982/how-to-remove-any-url-within-a-string-in-python  

7. https://www.reddit.com/wiki/markdown 

8. https://www.reddit.com/r/announcements/comments/7a4bjo/time_for_my_quarterly_inquisition_reddit_ceo_here/dp70sul/?context=2

9. https://en.wikipedia.org/wiki/Naive_Bayes_classifier

10. https://stackoverflow.com/questions/29867367/sklearn-multinomial-nb-most-informative-features

11. https://scikit-learn.org/stable/modules/tree.html#minimal-cost-complexity-pruning

12. https://stackoverflow.com/questions/11331982/how-to-remove-any-url-within-a-string-in-python
