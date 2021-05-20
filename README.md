# Fraud_Detection

## Introduction
This project is to build machine learning models to predict the probability that an online transaction is fraudulent, as denoted by the binary target “isFraud”. 
After merging the provided datasets, we got one large-scale train dataset to manipulate, which contains 590,540 rows and 434 features.

## Main Challenges and how we tackle these challenges:

Enormous Data: As transaction data is processed every day and the model build must be fast enough to respond to the scam in time. So, we build a LightGBM model with both low running time and good performance.

Imbalanced Data: most of the transactions (99.8%) are not fraudulent which makes it hard for detecting the fraudulent ones. So, we try to tune the LGBM model to minimize both false negatives (FN) and false positives (FP), and we present this in a Normalized Confusion Matrix.

## System Pipelines

Data Preprocessing: Since we have large datasets with huge number of rows and columns, data preprocessing is required.
• We clean both train_transaction and train_identity before emerging two dataframes.
• There are a lot of missing values on train_transaction.csv. If the percentage of missing value is more than 0.9, we drop the column.
• If the percentage of missing values is small and the column contains numerical values, we replace the missing values with median since the column is not normally distributed most of the time. There is the skewness.
• When the column contains categorical values, we covert each values in a column to a number.
• ‘R_emaildomain’ , ‘P_emaildomain’- we manually group emails when the email has the same value. For example, we replace ‘yahoo.com.mx’ and ‘yahoo.co.jp’ by ‘yahoo.com’. We covert each value to a number after grouping them together.
• On train-identity dataframe, ‘DeviceInfo’ column contains too many categories so we predict top 20 devices and replace top 10 by 1 to 10. We replace other categories by 11.

## Algorithm

In the modeling part, we tried three algorithms: decision tree, and light gradient boosting machine.

• A decision tree was built with default hyperparameters in the first place. The testing AUC score is only about 0.75.
• We tried LightGBM model with default hyperparameters. The testing AUC score is above 0.94, and it runs much faster.
• Then we fine tune our LightGBM hyperparameters, a finally we get an average testing AUC score to be above 0.98 after 5-fold validation. 

