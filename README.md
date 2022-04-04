# LightFM-recommendation-System
Code for LightFm recommendation system for Interview

* As my local setup is not able to handle high computational requirements I have completed the whole assignment on the Kaggle notebook so the codebase is in form of Jupyter notebooks. The code can be easily converted into python class function format from the notebook. I have commented on most of the steps in the Jupyter notebook and the Kaggle link provided below.

* Also only 1 million interaction data was used for recommendations created as the whole task was time-consuming in nature.

* During splitting of the dataset for each user the percentage is kept 75:25 as train and test respectively order by DateTime rather than absolute division of dataset on DateTime.

* Notebook folder contains two Notebook : </b>
   1. One for EDA, Processing and Cleaning 
   2. For Implementing a recommendation system using LightFM.

* Recommendation of 1k test users is saved in the Output folder


1. EDA, Processing and Cleaning: https://www.kaggle.com/parthplc/interview-eda-visualization-and-data-cleaning </b>

2. Implementing recommendation system using LightFM: https://www.kaggle.com/parthplc/interview-building-recommendation-system-lightfm

3. Output: https://docs.google.com/spreadsheets/d/1ZNJwlPuSW9NsGSdq4cG67f5yRoRZ72qPj1MxIjw64CA/edit?usp=sharing



# Interview Questions


## Which model to choose ? 

* Recommendation system can be mainly divided into three categories: Collaborative Filtering ( based solely on interaction ), Content-based (based on content features collected in past) and Hybrid recommendation (combining both content and collaborative features). Since the data provided was mostly interaction-based with only category type being the only content-based feature building a content-based recommender system is not possible.

* Collaborative Filtering could be used but one major problem of collaborative filtering is a "cold start". Users with very small history or no history get no recommendation in this case.

* Hybrid recommender system is a special type of recommender system that combines both content and collaborative filtering method. We only have content-based features of the item i.e. pratilipi in the given dataset so in addition to the interaction we will also provide item features to the recommender system thus making the hybrid recommender the best choice.

</b>

Now that we know a Hybrid recommender system is the best choice.If we have a glance at the dataset provided we don't have any ratings or equivalent matrix for determining how much a user like a pratilipi. So we don't have explicit feedback to feed into our recommender function. So we will use "read_percent" as our only implicit feedback and we need a recommender system will is very good at working with implicit feedback. LightFm is one such model. Let's understand why?

## What is LightFM?

* LightFM is a hybrid matrix factorisation model representing users and items as linear combinations of their content features’ latent factors. The model outperforms both collaborative and content-based models in cold-start or sparse interaction data scenarios (using both user and item metadata) and performs at least as well as a pure collaborative matrix factorisation model where interaction data is abundant.

## Why did you choose this model: LightFM? 

* In both cold-start and low-density scenarios, LightFM performs at least as well as pure content-based models, substantially outperforming them when either (1) collaborative information is available in the training set or (2) user features are included in the model.

* When collaborative data is abundant (warm-start, dense user-item matrix), LightFM performs at least as well as the Matrix factorization model.

* Also the model is easy to use and deploy in production and also at my previous company we deployed this model which in the real world was also giving good results.


## Implementation of Lightfm

* Implementation of light was done using LightFM Python Library by lyst. It is a really well-maintained library that is used in production by many well-reputed brands. Also, it provides an inbuilt metric of evaluation for the LightFm model. </b>


* Lightfm library also provides us a very popular matrix factorization method known as WARP. It works well for implicit feedback which was the initial problem we had with the dataset!


## Evaluation

*  AUC score : 0.8793001
*  Precision at k : 0.00756035
*  Mean Reciprocal Rank : 0.03175921
*  Recall at k : 0.023029210806254596
* Jaccard : 0.1664178367947089

We could also use NDCG and other sophisticated metrics for the evaluation of the model.

## Improvements

* The data provided was in abundance but due to a shortage of computing resources, the total interaction dataset was very small. This is also reflected in the test metric calculated above. Usually, for production, the dataset size would be much higher.

* During EDA we do find several outliers in reading time but those were not removed due to a lack of understanding of why such reading time exists. Removing outliers before recommending becomes very essential.

* No user feature was provided like demographic features, gender, age or other thus the user_feature feed to the LightFm model was empty. This led to poor results in test metrics. The same can be said about authors of pratilipi. We do not have their popularity indexes such as the number of followers or total view on combined pratilipis.

* Content-based features should have more depth than just the category. we can encode a summary of each pratilipi into a single feature for a better understanding of the content. Encoding the titles of each pratilipi could also give improvement to the model.

* Also feature representing monthly, yearly and weekly trend can also be included.

* Apart from dataset improvements, the model hyperparameter is not finetuned for the use case during training. Also, training was limited to 200 epochs due to slow training. (which is very low)

* Metric used for evaluation can also be created as per our requirement. 

* No available evaluation metric is a strong indicator for the recommender system performance in the real world scenario. What we could do is a real-world AB test on a small cohort of users and check if our model is affecting the engagement positively. We could also incorporate findings of previously deployed models into our current model.



