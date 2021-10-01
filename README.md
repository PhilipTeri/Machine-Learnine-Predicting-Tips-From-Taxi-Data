# Machine Learning - Predicting Tips From Taxi Data

#### Purpose

The purpose of this project is to use existing taxi data to train a machine learning model that predict how much a rider will tip. I used the K-Nearest Neighbors, Random Forest and Linear regression algorithms to make predictions.


### Data Wrangling

The data is from the Taxi and Limousine Commission of New York City. Each month is published as a csv file, so I took three months from 2017: March, June, and November. Each month contained around 10 million entries. The merged dataframe contains 29236424 row and 17 columns.

### Data Cleaning

The only columns in the dataframe that should have a value of 0 is the tip column and the extra column. Everything else should have a value greater than 0. For example there were many columns with trip distance set to 0, this is likely due to someone cancelling their trip and still being charged the minimum fee. All rows with values containing 0 are removed. 

### Exploratory Data Analysis

I took a sample of 100k rows from the original 29 million, it was taking too long to load the table and create graphs from the data. 

![image](https://user-images.githubusercontent.com/41071502/135649382-3d7a5aa7-2bd5-466e-ac91-9a3b9f96a257.png)

I plotted the histograms of all columns. This is a good way to find obvious issues with the data. For example I can tell that the mta_tax and improvement_surchage columns are likely set rates. This will not add additional information, so they are removed. 


![image](https://user-images.githubusercontent.com/41071502/135649833-6004b75f-debe-428f-bf51-bd4f1f7f7e4c.png)

It is also useful to look at the statistical correlation between all features. This may point out some strong correlations in the data. There is a very strong correlation between tip amount and total ammount, so one early thought I had is that maybe tips are mostly determined as a percentage of the trip cost, similar to dining at a restaurant. 

![image](https://user-images.githubusercontent.com/41071502/135650270-edeec2d3-16dc-408b-a0eb-231d6fd9b16f.png)

I plotted scatter plots of each column and the tip_amount columns. One major discovery from this is that there are negative values for the columns: 'fare_amount', 'extra', and 'total_amount'. This is due to charge backs, so these columns are removed. Another thing I noticed is that there is no variance in tip ammount for other payment types. I then figured out that only credit/debit payments tracked tipping, cash and other payment types were not documented, so I removed all rows with other payment methods. This is a major change in the project since now I am only predicting tipping from riders who paid with a card.


### Pre Processing

I removed all object and datetime columns from the database. I was initially going to create a feature for trip time but later thought it may be redundant since I already have trip distance. I also dropped the payment type at this point since all of our rows are now using the same payment method. 

I then used the pd.get_dummies() method to encode any categorical data. 

I created the X and y variables. X being the dataframe excluding the tip columns and y being just the tip column. Then I split the data into training data and test data sets, I used a 75% training and 25% test split. GridSearchCV was used to determine the optimal number of neighbors for the KNN algorithm and the number of estimators for the random forest algorithm. 

The pre processing for the Linear regression algorithm was slightly different. I still used a 72/25 split but I had to reshape the X variable. 


### Results

Below are the results for each algorithm.

<br>KNN Accuracy Score : 0.6151906839009164.
<br>Random Forest Accuracy Score: Score: 0.9346512465484813.
<br>Linear Regression Coefficient of Determination: 0.44896589290159583.

![image](https://user-images.githubusercontent.com/41071502/135657500-5a0ea412-30ba-4da3-b35e-5f3e33826f94.png)

Random forest performed the best of all of the algorithms, so I used it to determine feature importance. The graph below shows the imporance of each feature relative to eachother.

### Future Improvements

<br>• See if I can find data on tipping using different payment methods.
<br>• Try adding the time of trip feature and see if it makes a difference.
<br>• Use more data, try running this for a whole year rather than a sample from 3 months. 




