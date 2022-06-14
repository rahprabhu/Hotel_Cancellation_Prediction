# Predicting Hotel Cancellations

## Background

In this project, I will be working with a dataset containing reservation data for a hotel in Lisbon, Portugal and a resort hotel in the Algarve region of Portugal. The dataset contains features such as the the length of stay, price, lead time, booking channel, and more. For more information on the data, the link to the dataset and the link to the data dictionary are below.

[Data Source: Kaggle](https://www.kaggle.com/datasets/jessemostipak/hotel-booking-demand) <br>
[Data Dictionary](https://www.sciencedirect.com/science/article/pii/S2352340918315191)

**Project Goal**: To predict reservation cancellations. The target variable is binary variable that indicates whether the reservation was cancelled or not, so to predict this value, we will use classification methods such as **Logistic Regression**, **Random Forest Classifier**, and **XGBoost Classifier**. The primary scoring metric that I will use to compare models is the recall score for cancelled reservations. The recall score, or true positive rate, will tell us what percentage of cancelled reservations we predicted correctly. 


## Analysis Steps

### Data Processing and EDA
The dataset has many categorical features, so most of the processing steps go towards transforming the categorical features to be numerical so that they can be properly handled by the machine learning models. I primarily use label encoding or frequency encoding to transform these features, opting to limit the usage of one-hot encoding to reduce the dimensionality and sparsity of the dataset. Some key findings from the EDA include:
- 63% of the reservations were not cancelled, 37% were cancelled. Not quite an imbalanced dataset, but certainly favoring non-cancelled reservations.
- Guest most often stays at the hotel for 2 nights
- Seasonality is present in reservations and cancellations. Reservations and cancellations peak during the summer months and are lowest during the winter months.
- Almost 100% of non-refundable reservations were cancelled. Maybe the hotels should consider offering less non-refundable reservations or offer them at a discounted rate.
<br>
<br>

### Feature Selection, Classification Modeling, Model Evaluation
To select features for the models, I use correlation and mutual information. The correlation method enabled me to remove any features that showed strong collinearity, while the mutual information method helped in removing features that provide little to no information gain and show a low dependency with the target. After performing the feature selection, I ran the 3 classification models and compiled the accuracy, precision, and recall scores in a dataframe. Below are the scores. <br>
<br>

![image](https://user-images.githubusercontent.com/100224330/173500466-9ae98762-a9ed-49f3-9055-afbc98b554f8.png)<br>
<br>

The Random Forest and XGBoost models performed similarly as far as accuracy is concerned, but the XGBoost model performed slightly better when it comes to recall. We ideally would like to have greater recall for our models, but the XGBoost model performs well enough to be informative for the hotels to identify potential cancellations and proactively reach out to the guests with reminders or additional deal sweeteners to reduce the likelihood they cancel. Below is the chart showing which features were the most important to the model.

![image](https://user-images.githubusercontent.com/100224330/173502953-11d5ba50-c8e0-4e31-8e4c-9df2d91e4be3.png)

The 3 most important features are the deposit type, the # of required parking spaces and the guest being from Portugal.
- Not having a deposit down for a hotel room likely frees the guest up to consider other accomodations without penalty, so the importance of the deposit type makes sense. 
- Arranging for required parking spaces likely suggests a guest is highly intent on visiting, or perhaps has more concrete travel plans that would be more difficult to cancel.
- For people in Portugal, travel plans are likely less cumbersome than those of guests from out of the country, so it's understandable that Portuguese guests could more easily cancel their reservations. To maximize the high-likelihood guests, the hotel group could look to do more advertising and promotion in other top guest origins outside of Portugal. To minimize the risk of losing local guests, the hotel group could run more promotional rates and look to offer some sort of loyalty rewards.
