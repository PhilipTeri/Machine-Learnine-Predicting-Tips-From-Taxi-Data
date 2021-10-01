# Machine Learning - Predicting Tips From Taxi Data

#### Purpose

The purpose of this project is to use existing taxi data to train a machine learning model that predict how much a rider will tip. 


### Data Wrangling

The data is from the Taxi and Limousine Commission of New York City. Each month is published as a csv file, so I took three months from 2017: March, June, and November. Each month contained around 10 million entries. The merged dataframe contains 29236424 row and 17 columns.

### Data Cleaning

The only columns in the dataframe that should have a value of 0 is the tip column and the extra column. Everything else should have a value greater than 0. For example there were many columns with trip distance set to 0, this is likely due to someone cancelling their trip and still being charged the minimum fee. All rows with values containing 0 are removed. 

### Exploratory Data Analysis

![image](https://user-images.githubusercontent.com/41071502/135649382-3d7a5aa7-2bd5-466e-ac91-9a3b9f96a257.png)
