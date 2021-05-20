# Fraud_Detection

## Introduction
This project is to build machine learning models to predict the probability that an online transaction is fraudulent, as denoted by the binary target “isFraud.” 
After merging the provided datasets, I got one large-scale train dataset to manipulate, which contains 590,540 rows and 434 features.

## Main Challenges and how I tackle these challenges:

Enormous Data: As transaction data is processed every day and the model build must be fast enough to respond to the scam in time. So, I build a LightGBM model with both low running time and good performance.

Imbalanced Data: most of the transactions (99.8%) are not fraudulent, making it hard to detect fraudulent ones. So, I try to tune the LGBM model to minimize both false negatives (FN) and false positives (FP), and I present this in a Normalized Confusion Matrix.

## System Pipelines

Data Preprocessing: Since I have large datasets with a huge number of rows and columns, data preprocessing is required.
• I clean both train_transaction and train_identity before emerging two dataframes.
• There are a lot of missing values on train_transaction.csv. If the percentage of missing value is more than 0.9, I drop the column.
• If the percentage of missing values is small and the column contains numerical values, I replace the missing values with median since the column is not normally distributed most of the time. There is the skewness.
• When the column contains categorical values, I covert each value in a column to a number.
• ‘R_emaildomain,’ ‘P_emaildomain’- I manually group emails when the email has the same value. For example, I replace ‘yahoo.com.mx’ and ‘yahoo.co.jp’ by ‘yahoo.com.’ I covert each value to a number after grouping them together.
• On train-identity dataframe, ‘DeviceInfo’ column contains too many categories, so I predict the top 20 devices and replace the top 10 by 1 to 10. I replace other categories by 11.

## Algorithm

In the modeling part, I tried three algorithms: light gradient boosting machine.

• I tried the LightGBM model with default hyperparameters. The testing AUC score is above 0.93, and it runs much faster.

![Figure1](https://user-images.githubusercontent.com/49568184/118905362-8b5dc080-b8e9-11eb-90f9-086405dd7c54.jpg)

• Finally, I get an average testing AUC score to be above 0.98 after 5-fold validation. 

