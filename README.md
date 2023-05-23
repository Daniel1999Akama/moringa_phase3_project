# Phase 3 project
# SyriaTel Telecommunication Company Churn Prediction

## Project Overview
SyriaTel is a telecommunications company that prides itself in offering top-notch services to their customers. They are the leading telecoms company in their country and want to remain the leader in that particular sphere. Over the years they have chartered alot of the strides in technology in their country and want to continue improving.

# 1.Business Understanding
Stakeholders: SyriaTel executives and managers.

## Problem Statement
In a bid to continue leading SyriaTel is facing a significant challenge, CUSTOMER CHURN i.e where the customers are discontinuing their services and switch to other service providers. This churn not only leads to revenue loss but also affects the company's market position and customer satisfaction.

## Proposed Solution
The proposed solution is to develop a machine learning model that can analyze customer data, including demographics, usage patterns, service subscriptions, to predict the likelihood of customer churn. The model should be able to identify customers who are most likely to churn, enabling the telecommunication company to take proactive measures to retain them.

## Project Objectives
1. To develop a model that will help in predicting if a customer churns or not based on various attributes.
2. To identify the attributes that heavily impact if a customer churn's.

## Project scope and limitations
1. This project was ochestrated as an extra advisory tool to support top-level management make informed decisions to deal with customer retention.
2. The project outputs i.e.the model will not be realized as a full application with a user interface but rather a final report on the findings based on the data used which include a number of recommendations.
3. Internal data from the company will be the primary data source that will drive this project.
4. Ultimately the final steps taken to mitigate the situation is upto the company.

## Benchmark metric
* The bench mark evaluation metric that will be used in this project is ACCURACY.
> * Justification: from objective 1 we want to know if a customer churns therefore accuracy and F1 score would be suitable.
* F1-score is also considered but not the main metric.

# 2.Data Understanding
Here we will explore the data to get a better understanding of its state, then decide on the steps we need to take to clean it. We will begin by defining a class for the following tasks:
* getting the shape of the data
* getting data info
* descriptive stats

Sample dataset

![alt text](https://github.com/Daniel1999Akama/moringa_phase3_project/blob/master/sample_dataset.jpg)

From the class describer, the dataset has:

* 3333 customers.
* 21 customer features: 4 string predictors, 16 numeric predictors and the target.
* Various transformations will be applied on the dataset both for analysis and modeling e.g type conversions, feature seleciton etc.

# 3. Data Preparation
Summary on data preparation.
* The Data has no missing values.
* The Data has no duplicates.
* The unique column Phone Number has no duplicates
* Outliers were not be removed. See justification in notebook.

# 4. Exploratory Data Analysis
In this section, we will explore univariate EDA and bivariate EDA.
* Overall churn ratio.
* Churn against states.
* Churn against international plan.
* Churn against voice mail plan.
* Churn against number of customer service calls.

Overall churn ratio.
![alt text](https://github.com/Daniel1999Akama/moringa_phase3_project/blob/master/univariate.jpg)

Bivariate analysis.
![alt text](https://github.com/Daniel1999Akama/moringa_phase3_project/blob/master/bivariate.jpg)

# 5. Preprocessing
* In this section we will prepare the data for modeling.
* Some of the preprocessing that will take place here include:
> * Feature selection.
> * Train test split.
> * Encoding: dummy encoding and basic replace application.

## 5.1. Feature selection
* Here we investigate the important features of the data set and choose them to reduce complexity of the models ergo avoiding overfitting from the get go.
* The criteria used to select relevant columns is domain knowledge and feature importance analysis provided by decision trees..
* Based on telecom domain knowledge, the following features may be relevant for churn prediction:
> * state - The geographic location of the customer could potentially play a role in churn behavior, as different states may have varying levels of competition, coverage, or customer preferences.
> * account length - The duration of the customer's account with the telecom company may provide insights into customer loyalty and the likelihood of churn.
> * international plan - This feature indicates whether the customer has an international calling plan.
> * voice mail plan and number vmail messages - These features capture whether the customer has a voicemail plan and the number of voicemail messages.
> * customer service calls - The number of customer service calls made by the customer could indicate dissatisfaction or issues that may lead to churn.
> * 'total day minutes', 'total day calls', 'total day charge', 'total eve minutes', 'total eve calls', 'total eve charge', 'total night minutes', 'total night calls', 'total night charge', 'total intl minutes', 'total intl calls', 'total intl charge': These features represent the usage and charges for different time periods (day, evening, night, international). Usage patterns and charges across different time periods can provide insights into customer behavior and preferences.

# 6. Modelling
* In this section is where the magic happens.
* The problem at hand is a classification problem.
* We will explore 3 models: a baseline DecisionTreeClassifier, a randomforest classifier and a tuned random forest model.
* Model accuracy and F1 score will be the metrics for evaluation.
> * Justification: Accuracy to get a verdict if a customer churns or not. F1 score to get a balance between precision and recall.

* Accuracy of 70% and F1 score of 70% will be the threshold to deam the model as successful.

## Building a regular tree as a baseline
> Feature importance
![alt text](https://github.com/Daniel1999Akama/moringa_phase3_project/blob/master/states.jpg)

### Evaluation of baseline model
#### Machine Learning Communication - baseline model
<b>Rationale why modeling was implemented.</b>
* While simpler forms of data analysis, such as descriptive statistics or basic data visualization, can provide initial insights, they may not be sufficient for complex problems or large datasets. Machine learning leverages advanced algorithms to uncover hidden patterns.
<b>Results.</b>
> * Accuracy on the training set: 1.0
> * F1 score of the model on train set: 1.0
> * Accuracy on the testing set: 0.92
> * F1 score of the model on test set: 0.75
> * The model is overfitting
> * The accuracy means that the model can predict with an accuracy of 92% whether a customer will churn or not.
> * From the graph one can see how each predictor was important in modeling.
<b>Limitations of baseline model.</b>
* The current model is not fit for prediction since it is not generalizing well to new data even with high accuracy. The model is overfitting.
* This we see from the 7% difference between train and test accuracy.
* This we see from the large difference between train and test F1-score

## Model 2: Basic Random Forest Model
> Feature importance
![alt text](https://github.com/Daniel1999Akama/moringa_phase3_project/blob/master/3.jpg)
#### Machine Learning Communication - random forest model
<b>Rationale why ensemble modeling will be implemented.</b>
* While simpler forms of data analysis, such as descriptive statistics or basic data visualization, can provide initial insights, they are not sufficient for complex problems or large datasets such as this one. Ensemble models leverages advanced algorithms to uncover hidden patterns, make accurate predictions, and provide actionable insights that can greatly benefit SyriaTel in decision-making processes.
<b>Results.</b>
> * Accuracy on the training set: 0.92
> * F1 score of the model on train set: 0.73
> * Accuracy on the testing set: 0.89
> * F1 score of the model on test set: 0.69
> * The model is not overfitting but it is exhibiting issues because the test scores are higher than train. This may be due to data leakage, random variations or training size.
> * The accuracy means that the model can predict with an accuracy of 89% whether a customer will churn or not.
> * From the graph one can see how each predictor was important in modeling.
<b>Limitations.</b>
* The current model is not fit for prediction since it is experiencing higher test scores indicating internal issues e.g random variations, data leakage etc.
* This we see from the difference between train and test accuracy.
* This we see from the difference between train and test F1-score.

## Model 3: Tuned Random Forest Model
* Building a model using grid searchCV to find best set of hyper-parameters.
* Different from base model and Model 2 in that we employ an ensemble model with grid searchCV to find the best set of hyperparameters to battle overfitting while improving accuracy and F1 score.
* Employing SMOTE to handle the imbalance issue and scaling down of features also to battle overfitting.
* Employing cross validation to tackle the random variation issue.
>Feature importance
![alt text](https://github.com/Daniel1999Akama/moringa_phase3_project/blob/master/3.jpg)
#### Machine Learning Communication - tuned random forest model
<b>Rationale why tuned ensemble modeling will be implemented using grid searchCV.</b>
* While simpler forms of modelling and data visualization, can provide initial insights, they are not sufficient for battling overfitting. Grid search and tuned Ensemble models leverages advanced algorithms to uncover hidden patterns, make accurate predictions, provide actionable insights and battle overfitting by finding the best set of hyperparameters. This greatly benefits SyriaTel in decision-making processes.
<b>Results.</b>
> * Accuracy on the training set: 0.93
> * F1 score of the model on train set: 0.78
> * Accuracy on the testing set: 0.92
> * F1 score of the model on test set: 0.74
> * The model is not overfitting. It is now performing as expected.
> * The accuracy means that the model can predict with an accuracy of 92% whether a customer will churn or not.
> * From the graph one can see how each predictor was important in modeling.
The current model is fit for prediction since the difference between train and test scores is proper.
This we see from the difference between train and test accuracy.
This we see from the difference between train and test F1-score.

# 7. Findings, Recommendations and next steps.
Outlined in the notebook













