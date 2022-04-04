# LightFM-recommendation-System
Code for Lightfm recommendation system for Interview

* As my local setup is not able to handle high computational requirements I have completed the whole assignment on Kaggle notebook so the codebase in form of jupiter notebook. The code can be easily converted into python class function format from notebook. I have commented most of the steps in the jupiter notebook and Kaggle link provided below.

* Also only 1 million interaction data was used for recommendation created as the whole task was time consuming in nature.


* Notebook folder contains two Notebook : </b>
   1. One for EDA, Processing and Cleaning 
   2. For Implementing recommendation system using LightFM.

* Recommendation of 1k test users is saved in  Output folder


1. EDA, Processing and Cleaning : https://www.kaggle.com/parthplc/interview-eda-visualization-and-data-cleaning </b>

2. Implementing recommendation system using LightFM : https://www.kaggle.com/parthplc/interview-building-recommendation-system-lightfm

3. Output : https://docs.google.com/spreadsheets/d/1ZNJwlPuSW9NsGSdq4cG67f5yRoRZ72qPj1MxIjw64CA/edit?usp=sharing



# Interview Questions


## Which model to choose ? 

* Recommendation system can be mainly divided into three parts : Collaborative Filtering ( based solely on interaction ),Content based (based on content features collected in past) and Hybrid recommendation (combining both content and collabrative features). Since the data provided was mostly interaction based with only category type be the only content based feature building a content based recommender system is not possible.

* Collaborative Filtering could be used but one major problem of collaborative filtering is "cold start". User with very small history or no history get no recommendation is this case.

* Hybrid recommender system is a special type of recommender system that combines both content and collaborative filtering method. We only have content based feature of the item i.e. pratilipi in the given dataset so in addition to interaction we will also provide item features to recommender system thus making hybrid recommender best choice.

</b>

Now that we know Hybrid recommender system is the best choice.If we have a glance on dataset provided we don't have any ratings or equivalent matrix for determining how much a user like a pratilipi. So we don't have explicit feedback to feed into our recommnder function. So we will use "read_percent" as our only implicit feedback and we need a recommender system will is very good on working with implicit feedback. Lightfm is one such model. Lets understand why ?

## What is LightFM?

* LightFM is a hybrid matrix factorisation model representing users and items as linear combinations of their content features’ latent factors. The model outperforms both collaborative and content-based models in cold-start or sparse interaction data scenarios (using both user and item metadata), and performs at least as well as a pure collaborative matrix factorisation model where interaction data is abundant.

## Why you choose this model : LightFM ? 

* In both cold-start and low density scenarios, LightFM performs at least as well as pure content-based models, substantially outperforming them when either (1) collaborative information is available in the training set or (2) user features are included in the model.

* When collaborative data is abundant (warm-start, dense user-item matrix), LightFM performs at least as well as the Matrix factorization model.

* Also the model is easy to use and deploy in production and also at my previous company we deployed this model which in real world was also giving good results.


## Implementation of Lightfm

* Implemntation of lightfm was done using LightFM Python Library by lyst. It is really well maintained library that are used production by many well reputed brands. Also it provide inbuilt metric of evaluation for the lightfm model. </b>


* Lightfm library also provide us a very popular matrix factorization method known as WARP. It works really well for implicit feedback which was the initial problem we had with the dataset!


## Evaluation

*  AUC score : 0.8793001
*  Precision at k : 0.00756035
*  Mean Reciprocal Rank : 0.03175921
*  Recall at k : 0.023029210806254596
* Jaccard : 0.1664178367947089

We could also use NDCG and other sophisticated metric for evaluation of model.

## Improvements

* The data provided was in abundance but due to shortage of compute resources the total interaction dataset was very small. This is also reflected in test metric calculated above. Usually for production the dataset size would be much higher.

* During EDA we do find several outliers in reading time but those were not removed due to lack of undersatnding on why such reading exists. Removing outliers before recommending becomes very essential.

* No user feature was provided like demographic features,gender,age or other thus the user_feature feed to lightfm model was empty. This led to poor result in test metric. Same can be said by about authors. We do not have their popularity index such as number of followers or total view on combined pratilipis.

* Content based feature should have more depth than just the category. we can encode a summary of each pratilipi into a single feature for better understanding of the content.

* Also feature representing monthly,yearly and weekly trend can also be included.

* Apart from dataset improvements, the model is not finetune for the usecase during training. Also training was limited to 200 epoch(which is very low.)

* Metric used for evaluation can also be created as per our requirement. 

* Although we have several eveluation metric available for recommender system but the best metrics is doing a real world AB test on small cohort of users. We could also incorporate finding of previously deployed models in our current model.



