# Kaggle_Predict_Future_Sales

### Overview

The objective of the project is to predict total sales for every store-item combination for 1C Company by analyzing the historic time-series data
 - Data: Daily historical data for the period: Jan’13 to Oct’15
 - Objective: Predict Nov’15 sales for shop-item combinations
 - Evaluation Metric: RMSE

The time-series data from 1C Company is composed of 5 datasets capturing the items data, item categories data, shops data, sales training data, and test data

The below approach was adopted to solve the problem:
 - In-depth Exploratory Data Analysis
 - Feature Engineering
 - Applying models (with parameter optimization) for the best results
 
 

### List of Features

 - Date based features (Month, Count of weekends/ weekdays per month) -> To capture seasonality in the data
 - Expanding mean-encoding based features based on item count: Features encoded on: item_id, shop_id, item_category_id, and master category id -> It is used to capture linear   relationships between label and target. Expanding mean encoding is implemented regularization (avoid overfitting)  
 - Aggregation based features based on avg. item price: Features encoded on: item_id, shop_id, item_category_id, master category id and shop-item category key -> Considering the observation that particular combinations have more sales, aggregation based features were added and these features were used as lag variables for the analysis
 - Aggregation based features based on avg. item count & item count sum: Features encoded on: item_id, shop_id, item_category_id, master category id and shop-item category key ->  Considering the observation that particular combinations have more sales, aggregation based features were added and these features were used as lag variables for the analysis
 - Lag features for month 1,2,3,4,5,6,12 for numeric features -> Lag features are added in-line with the simple window method. It was observed that the recent 6M sales have more impact on future sales, and 12M lag was added to capture seasonality
 - Delta Lag features for month 1 and month 2 -> Given the time-series, it is expected that previous sales changes (highs/ lows) would impact future sales

### Insights (XGBoost Model)
 - Lags 1-3 seem to be the most important lag features suggesting a relation between recent month sales on future sales
 - Item count aggregates and lag features seem to be the most important features
 - Also, item id and item category id are important features which is in-line with the observation of some categories/ items showing high sales consistently
 - Item count delta price lag is also one of the important features suggesting that previous dip/ increase in sales impact future sales
 - As expected month number is an important feature in-line with the seasonal nature of the data
 - The feature capturing number of weekends/ weekdays isn’t an important feature; therefore, the peak in sales during weekends may not be generalizable

  
 

