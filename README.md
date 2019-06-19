# ![](https://ga-dash.s3.amazonaws.com/production/assets/logo-9f88ae6c9c3871690e33280fcf557f33.png) Project 3: Web APIs & Classification


# Problem Statement:


Our consulting firm, JL Consulting Group, was hired by YG Entertainment, a company based in South Korea that operates as a record label, talent agency, music production company, event management, concert production company, and music publishing house. YG Ent. realized the Korean popular music industry (Kpop) is becoming heavily saturated with countless new Kpop groups debuting left and right. Many of these groups are backed by their also newly formed agencies. YG Ent., as well as many other top Kpop agencies, believe the future of Kpop is world-wide exposure to foreign markets. Since over 10 years ago, YG Ent. launched many successful groups whose popularity broke barriers outside of Korea to Asia, parts of Europe and South America. However, the U.S. mainstream market seemed nearly impossible to break into, especially after Se7en's, a former YG solo act, unsuccessful American debut back in 2007. Now, 12 years later, YG has a girlgroup named 'Blackpink' and YG believes they will be able to make a much bigger impact in the U.S than any girlgroup in the history of Kpop. With the mindset of trying to avoid rushing into things, YG hired us to first analyze the Western online fanbase for Blackpink on [Blackpink subreddit](https://www.reddit.com/r/BlackPink/), to understand the organic response from the online community in order to help further drive the exposure of Blackpink and develop potential trends for future groups being able to broaden their own exposure and fanbase to the Western audience.


# Executive Summary

In order to accurately understand the words and language themes among the Western fanbase for kpop, and then try to interpret those words to see potential reasons for how or why they like Blackpink (even potentially over other kpop groups), we decided to include another Kpop group who has a huge following in America named 'BTS'. BTS is currently the leading kpop group that broke the standards of what breakout success looks like for kpop groups overseas. Today, BTS and Blackpink are the two most popular and influential kpop groups among the Western audience, respectively. As a result by collecting the most recent comments in the two subreddits, we will:

* Identify the words/language/themes that are common among Blackpink/Bts (or Kpop fans in general) fans in order to identify the two groups.
* Interpret those words/language/themes to help further Blackpink's success in the U.S.
* Interpret those words/language/themes to help develop potential trends for future YG groups seeking recognition in the U.S.

**01_Push_Shift_API notebook:**
We used the Push Shift API to collect 10,000 comments from the 'BlackPink' subreddit and 10,000 comments from the 'bantan' subreddit. We chose these two subreddits because both groups are the representatives when it comes to Kpop groups with breakout success in the West. At the time of the data collection, it was right before both groups made a comeback with an album. We chose this timeframe because the respective subreddits will become much more active and it will also encourage comments of those expressing feedbacks about the groups' past songs (what they liked/disliked about it) and excitement for the album (what they are excited or hopeful to hear). In addition to the soon to be released album, these two groups are currently on a world-tour (obviously including America), we hoped to gain some insight regarding this matter as well. 

**02_Cleaning_EDA notebook:**
We cleaned the data by removing certain comments. After plotting out the bar graph of each members' number of mentions, it turns out Lisa is the most mentioned member of Blackpink in our data, followed by Jennie, Jisoo and Rose. In many online platforms, there seems to be a general consensus acknowledging Lisa as the most popular Blackpink member *internationally*.
From searching the context of the comments containing 'lisa' as well as research in outside resource, we were able to derive a few assumptions as to the reason why Lisa is the more popular member:
* Lisa is the only *ethnically* foreign member of the group
* Lisa, along with Jennie, is the rapper of the group who portrays a *girl-crush* concept among female fans 
* Lisa has outstanding appearance and over-all talent (strong performer and the best dancer of the group)

**03_Preprocessing notebook:**
We preprocessed the data to have it set up for modeling. We identified 20 key words from each subreddit and interpreted a few of them to see what insights we can gain for the purpose of our problem statement and narrative.  
This is what we have interpreted so far:
* Many fans of Blackpink seem to have issues with the management of YG when it comes to handling Blackpink's promotion 
* Fans are frusterated over YG's lack of consistently promoting Blackpink throughout the year to capitalize on their popularity
* One the other hand, BigHit seems to be promoting Bts consistently throughout the year to capitalize on their current trend/success.

**04_Logistic_Regression_Model notebook:**
We tested and evaluated the Logistic Regression model. We originally tested a basic Logistic Regression model without inputting much parameters and unsurprisingly got a not-so-great score on our accuracy. Afterwards we created a pipeline that will consist to two stages:
* An instance of CountVectorizer
* A LogisticRegression instance

Through GridSearching for the optimal set of hyperparameters for our CountVectorizer, we got a Train accuracy score of 0.886 and
Test accuracy score of 0.765. A big improvement over the naive Logistic Regression model score. 
Through this model, we got the top 20 most important features:
* blinks, yg, vip, dddd, square, cf, ga, wig, whistle, scandal, queue, axe, d4, chanel, revolution, teddy, area, queens, diaries, aiiy

Confusion Matrix (shows how our model performed):
* True Negatives: 1795
* False Positives: 585
* False Negatives: 515
* True Positives: 1789

**05_Naive_Bayes_Model notebook:**
We tested and evaluated the Multinomial Naive Bayes model. We originally tested a *naive* Naive Regression model without inputting much parameters and surprisingly got a good score on our accuracy. Afterwards we created a pipeline that will consist to two stages:
* An instance of TFIDF Vectorizer
* A Multinomial N.B instance

Through GridSearching for the optimal set of hyperparameters for our TFIDF, we got a Train accuracy score: 0.843 and
Test accuracy score: 0.767. Not much of an improvement over the *naive* Multinomial N.B model score. 

Confusion Matrix (shows how our model performed):
* True Negatives: 1928
* False Positives: 452
* False Negatives: 635
* True Positives: 1669

**06_Random_Forest_Model notebook:**
We tested and evaluated the Random Forest model. We also created a pipeline that will consist of two stages:
* An instance of the TFIDF Vectorizer
* A Random Forest instance

Through GridSearching for the optimal set of hyperparameters for our Random Forest Model, we got a Train score: 0.984 and Test score: 0.717
The model clearly performed significantly worse on the testing set, with a 27% gap between the two scores. Although this is an improvement over the baseline model, the difference between this model's training/testing scores indicates a high variance and overfit model. However one thing to point out is that the Random Forest model works in minimizing the error on the training set; therefore, the accuracy score of the training set being higher than the score of the testing set is relatively expected. Nevertheless, further fine-tuning the hyperparameters through Randomized Search over GridSearchCV may have proven to be the better and more efficient choice. 

# Conclusion:
 
Our baseline prediction was 51% accuracy by predicting the majority class (BTS subreddit) for all comments.

The Logistic Regression model displayed strong improvement after finding better hyperparameters through GridSearch. By doing so we got a Train accuracy score of 0.886 and Test accuracy score of 0.765. The 20 most important features also provided the most useful insights when trying to understand the organic response from these fans in the Blackpink subreddit. 

The Multinomial Naive Bayes model performed relatively more consistently, compared to our other models, between the training and testing sets. It got a training score of 84% and a test score of 76%. Considering the simplicity of this *naive* model, this performed surprisingly well. 

The Random Forest model displayed a signficantly accurate performance with the training set; however, the same model performed badly on the testing set, indicating a huge possibility of high variance and overfitting. The predictive test accuracy score was only 71%, which is the lowest of all of our models.


# Recommendation:

* Consistent album release & activities to hold onto the short attention span of casual Kpop fans
* Experiment with different genres of music (Western influence → bubblegum pop, hip-hop, trap, ect.)
* Diversity → more fans!
* Build a connection with fans through personal broadcast videos 
