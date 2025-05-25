# Detection of Fake Accounts in Social Media Using Machine Learning

# Abstract
The rapid growth of social media platforms has led to an increase in fake accounts that engage in spam activities, spreading misinformation, and other malicious actions. To combat this issue, we propose a machine-learning model capable of distinguishing between real and fake user accounts. This project utilizes logistic regression, a well-established classification algorithm, to analyze user account features and predict their authenticity.The dataset used for training and testing the model comprises various account attributes, such as username characteristics, bio descriptions, number of posts, and followers. Exploratory Data Analysis (EDA) reveals significant patterns: fake accounts tend to have more numeric characters in their usernames, shorter bio descriptions, and minimal engagement in terms of posts and followers.The logistic regression model is implemented with and without regularization, demonstrating the impact of L1 and L2 penalty functions. Performance evaluation is conducted using Receiver Operating Characteristic (ROC) curves and Area Under the Curve (AUC) scores. The model without regularization achieves an AUC score of 96%, while the regularized model scores 77%, indicating slight overfitting in the latter.To further refine the model, GridSearchCV is used to optimize hyperparameters, enhancing predictive accuracy. The final model achieves an AUC of 93.9% on test data, confirming its reliability. The system also allows the platform management to set classification thresholds, giving them control over account suspension decisions based on model predictions. 

# Introduction 
The rise of fake accounts on social media platforms has become a significant issue, leading to spam, misinformation, and a degraded user experience. To address this, we developed a machine learning model to classify user accounts as either real or fake. This report outlines the steps taken, from data exploration to model evaluation, and presents the results of our efforts. 
  
# Problem Statement 
The goal of this project is to build a binary classification model that can distinguish between real and fake user accounts on a social media platform. The model will be trained on a dataset containing various features of user accounts, such as the ratio of numeric characters in usernames, length of descriptions, number of posts, and followers. The target variable is the fake column, where: 
+ 1 indicates a fake account.
+ 0 indicates a real account.

# Data Collection and Exploration 
The dataset used for this project is stored in social_media_train.csv. It contains the following key features: 
+ **ratio_numlen_username:** Ratio of numeric characters in the username to its length.
+ **len_desc:** Number of words in the account's bio description.
+ **ratio_numlen_fullname:** Ratio of numeric characters in the full name to its length.
+ **num_posts:** Number of posts by the user.
+ **num_followers:** Number of followers the user has.

# Key Findings from Exploratory Data Analysis(EDA) 
+ **Fake Accounts Characteristics:**
  - Fake accounts tend to have a higher spread in the ratio_numlen_username feature, while real accounts are clustered around the mean.
  - Fake accounts typically have fewer words in their bio descriptions (len_desc).
  - The average number of posts and followers for fake accounts is close to zero. 
+ **Correlation Between Features:**
  - ratio_numlen_username and ratio_numlen_fullname are moderately correlated (+0.4085).
  - Other features show weak correlations, which is ideal for logistic regression. 

# Model Development 
We used **Logistic Regression** as the primary algorithm for this classification task. Logistic regression is well-suited for binary classification problems and allows for regularization to prevent overfitting. 

**Approach:** 
+ **Without Regularization:**
  - A logistic regression model was trained without regularization (C=1e42) to establish a baseline.
  - The model achieved a high recall but lower precision, indicating it was better at identifying fake accounts but less reliable in its predictions. 
+ **With Regularization:**
  - A second model was trained with regularization (C=1.0) to improve generalization.
  - This model showed higher precision but lower recall compared to the nonregularized model. 
 
+ **Grid Search for Optimal Hyperparameters:**
  - We used GridSearchCV to find the best hyperparameters for the logistic regression model.
  - The optimal parameters were:
    * penalty='l2' (Ridge regularization).
    * C=4.92 (inverse of regularization strength).
  - The solver used was saga, which supports both L1 and L2 regularization. 
