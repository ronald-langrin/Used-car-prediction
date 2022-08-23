# Used-car-prediction

Context: 
There is a huge demand for used cars in the Indian Market today. As sales of new cars have slowed down in the    recent past, the pre-owned car market has continued to grow over the past few years and is now larger than the new car market. Cars4U is a budding tech start-up that aims to find foot holes in this market. In 2018-19, while new car sales were recorded at 3.6 million units, around 4million second-hand cars were bought and sold. There is a slowdown in new car sales and that could mean that the demand is shifting towards the pre-owned market. Infact, some car owners replace their old vehicles with pre-owned cars instead of buying a new automobile. Unlike new cars, where price and supply are deterministic and managed by OEMs (Original Equipment Manufacturer/except for dealership level discounts which come into play only in the last stage of the customer journey), the used car market is a very different beast, with large uncertainties in both pricing and supply. Several factors, including mileage, brand, model, year, etc. can influence the actual worth of a car. From the perspective of a seller, it is not an easy task to set the correct price of a used car. Keeping this in mind, the pricing scheme of these used cars becomes important in order to grow in the market.
The objective:
Due to the unprecedented number of cars being purchased and sold, used car price prediction is a topic of high interest. Because of the affordability of used cars in developing countries, people tend more purchase used cars. A primary objective of this project is to estimate used car prices by using attributes that are highly correlated with a label (Price). Come up with a pricing model that can effectively predict the price of used cars and can help the business in devising profitable strategies using differential pricing.
The key questions:

1. Why are they selling the car?
2. How old is the car?
3. What’s the car’s mileage?
4. How long have they owned the car?
5. What is the Brand and Model of the car?
6. What is the engine and power of the car?

The problem formulation:
Predict the price of cars in the Indian market. Predictions will be based on vehicle features such as power, engine, name, Location, age, make, model, mileage



Methodology

Load libraries

Load the data 

Understand the data by observing a few rows

Observations and Insights: 
There are both numerical and categorical variables in the dataset as such the categorical variables will have to be encoded. There are missing values in the new_price and price columns The name column contains data that may be able to be separated into different columns eg. "Mercedes-Benz E-Class 2009-2013 E 220 CDI Avan" contains year, brand name and model which may or may not be relevant Serial No. Also, may not be necessary as is too unique and maybe dropped later We also see both categorical and numerical variables which may influence the methods we use
Let us check the data types and and missing values of each column

Observations and Insights: 
Both categorical and numerical data can be seen. We will need to come up with ways to address the missing values as well, however al missing values appear to be numerical which will have to be addressed by some statistical means (mean, meadian, ect). The missing data seems minial compared to the number of rows in the dataset and a large missing value within the target variable is as expected
We can observe that S.No. has no null values. Also the number of unique values are equal to the number of observations. So, S.No. looks like an index for the data entry and such a column would not be useful in providing any predictive power for our analysis. Hence, it can be dropped.


Exploratory Data Analysis

Observations and Insights: 
The average year seems to be at 2013 Mileage minimum is at 0 which means that there is either outliers or incorrect data
Let us also explore the statistics of all categorical variables

Observations and Insights: 
most cars use either desisel or petrol. The least amount of cars are being sold in Ahmedabad. Most cars are manual transmission. Mahindra seems to be the top brand

Check Kilometers_Driven extreme values

Observations and Insights: 
In the first row, a car manufactured as recently as 2017 having been driven 6500000 km is almost impossible. It can be considered as data entry error and so we can remove this value/entry from data.

Check Mileage extreme values

Observations and Insights: 
Mileage of cars can not be 0, so we should treat 0's as missing values. We will do it in the Feature Engineering part.

Univariate Analysis - Numerical Data

Observations and Insights: 

Kilometers_driven is not normally distributed, it is right skewed. To solve this problem, the log transformation on kilometers_driven is applied when it has skewed distribution. And add the transformed variable into the dataset. You can name the variable as ' kilometers_driven_log'.

Like Kilometers_Driven, the distribution of Price is also highly skewed, we can use log transformation on this column to see if that helps normalize the distribution. And add the transformed variable into the dataset. You can name the variable as 'price_log'.

Like Kilometers_Driven, the distribution of Power is also highly skewed, we can use log transformation on this column to see if that helps normalize the distribution. And add the transformed variable into the dataset. You can name the variable as 'power_log'.

Univariate analysis - Categorical Data

Observations and Insights 
Most of the owners within this dat aset are first-time owners. Most cars are manual transmission cars. Diesel and Pertol is the predominant fuel type. Most care in the data set are "newer" cars (2011 - 2015)

Bivariate Analysis

Observations and Insights from all plots: 
Positive relationships:
•	price_log and year
•	power and engine
•	price_log and power_log
Coimbatore and Bangalore have on average the most expensive car prices
Diesel cars on average are the most expensive, electic cars although expensive are not significant in the data set. Automatic cars are the most expensive. Cars with only one previous owner are the most expensive


Feature Engineering¶

The Name column in the current format might not be very useful in our analysis. Since the name contains both the brand name and the model name of the vehicle, the column would have too many unique values to be useful in prediction. With 2041 unique names, car names are not going to be great predictors of the price in our current data. But we can process this column to extract important information for example brand name.

Missing value treatment

Missing values in Seats
extracted information from 'Name' column to impute missing values. Impute these missing values one by one, by taking median number of seats for the particular car, using the Brand and Model name.

Missing values for Mileage
replace zero to NAN as stated earlier. Impute missing Mileage. using median

Missing values for Engine
Impute these missing values one by one, by taking median number of engine for the particular car, using the Brand and Model name. Impute the rest missing Engine values using median

Missing values for Power
Impute these missing values one by one, by taking median number of power for the particular car, using the Brand and Model name. Impute the rest missing Power values using median

Missing values for New_price
left as is since this is a target variable

Added the column age
Age based on current Year

Observation on missing values 
New_Price, Price and Price_log is missing values as expected, Power_log is missing values as the log transformation needs to be done on the price column once again. To be addressed later


Potential techniques - What different techniques should be explored?

Encoding: In our dataset we have both categorical variables and  numerical variables (price column excluded). To apply the ML models, we need to transform these categorical variables into numerical variables. 

Normalization: The dataset is not normally distributed. We have used log transformation on price, power and kilometers_diven. Without normalization, the ML model will try to disregard coefficients of features that have low values because their impact will be so small compared to the big value. 

Train the data. In this process, 70% of the data can be split for the train data and 30% of the data can taken as test data.

Overall solution design - What is the potential solution design?

Linear Regression
Random Forest
XGBoost

Measures of success - What are the key measures of success?
Evaluate the best model Accuracy above 85%. 
