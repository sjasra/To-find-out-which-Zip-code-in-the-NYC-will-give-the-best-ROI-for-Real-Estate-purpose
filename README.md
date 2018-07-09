# To-find-out-which-Zip-code-in-the-NYC-will-give-the-best-ROI-for-Real-Estate-purpose

Business Problem: 
The real estate company has concluded that two-bedroom properties in New York City are the most profitable to invest in. however, they do not know which zip codes are best to invest. Based on the data provided, we need to find out which zip codes would generate the maximum profit on short term rentals with NYC (New York City).

How real estate company generates money?
As we are only considering the residential property here, we can assume the following two most common ways to profit from real estate investment:
	Cash flow from rental income
	Appreciation of a property

What Data we have?
	Cost data: Zillow provides us an estimate of value for two-bedroom properties.
	Revenue data: Airbnb is the medium through which the investor plans to lease out their investment property. We have the data from 1996 to 2017 which shows how much properties in certain neighborhoods rent out for in New York City.

Assumptions which are already given
	The investor will pay for the property in cash (i.e. no mortgage/interest rate will need to be accounted for).
	The time value of money discount rate is 0% (i.e. $1 today is worth the same 100 years from now).
	All properties and all square feet within each locale can be assumed to be homogeneous (i.e. a 1000 square foot property in a locale such as Bronx or Manhattan generates twice the revenue and costs twice as much as any other 500 square foot property within that same locale.)

My Assumptions
	I am assuming that real estate investors are trying to find out which properties are most profitable for the current year. i.e. year 2018.
	I am assuming “the profit on short term rentals” as the profit generated from rental over the initial investment amount in one year.

My 3 step Approach to solve the data challenge
	Step I: For each zip code in NYC, find out how much money could be generated from appreciation of property if we sell the property at the end of current year (i.e. 2018)
	Step II: For each zip code in NYC, find out how much Average Cash flow could be generated from the rental income for the current year 2018 for 2 Bedrooms properties.
	Step III: Find out what percentage of money could be generated in one year over the total initial amount investment.

Detail description of what I have actually done in these three steps

Step I: For each zip code in NYC, find out how much money could be generated from appreciation of property if we sell the property at the end of current year (i.e. 2018)
	I have read the zillows csv file in python program using pandas’ module. I have read the metadata and understood each dimension of the data.
	the following quality insights from the initial analysis of zillows data: 
	Price of properties from 1996-2009 have lots of missing values.
	Invalid data: In column “city”, there are so many bad entries which a City could not be.

	I have created a user defined function to preprocess a data. So that if new data comes in, It would be easy to preprocess it by just calling a function. In this function, I have selected the NYC data by applying filter on the “state” and “metro” columns. I have then selected the “year”, “zipcode” (RegionName) and “value” column from the data and dropped the rest. I have pivoted the columns for better analysis. then, I have found out the average value for each zip code for each year. 
	Created two machine learning Regressionpredictive models to predict the value for year 2018:
	Created Decision Tree and Linear Regression model
	Evaluated the performance of both the models on test data.
	Further, did K-Fold Validation to solve(Bias Variance trade off) and which model to be used for actual prediction,
	Decision tree model has found out to be the best fitted model after model comparison.
	I have predicted the actual values for 2018 by using decision tree repressor model.
	After predicting the value of the property for year 2018. I have calculated the increase or decrease in the property, which is nothing but the difference of value of a property in 2017 and 2018.
	I have created a calculated field for this increase of property which called “hike_in_one_year”.
	This column is nothing but the output which we were expecting from our Step I. i.e. how much money could be generated from appreciation of property if we sell the property at the end of current year.

Step II: For each zip code in NYC, find out how much Average Cash flow could be generated from the rental income for the current year 2018 for 2 Bedrooms properties.
	I have read the listing csv file in python program using pandas’ module. This file is nothing but the Airbnb data. I have read the metadata and understood each dimension of the data.
	Selected required columns and cleaned data of Airbnb.
	I have created a calculated field “rent earned per year” by multiplying the price by 273 (which is 75% of 365 days. This is because we are assuming the 75% occupancy of a property for short term rentals.)
	I have grouped the data by “zipcode” column and calculated the mean of “rent earned per year”. 
	The column “rent earned per year” is nothing but the output which we were expecting from our Step II. i.e. how much Average Cash flow could be generated from the rental income for the current year 2018 for 2 Bedrooms properties.

Step III: Find out what percentage of money could be generated in one year over the total initial amount investment.
	I have created a calculated field called “profit percentage” which is a total amount earned in a year through rentals and appreciation over the total amount invested for initial buying of a property.
	I have used following formulae for the calculation of this field “profit percentage”
	
"profit percentage"=(""rent_earned per year\""+ hike_in_one_year" )/"value"

Conclusion
I have concluded the best zip code for investment as the zip code 10312. As, it has capability of generating highest percentage of profit over the short period of time.



After else could have been done:

	If I could get Zillows properties dat from 1996 of good quality and with extra features then Artifical Neural network could have been used.
	Animated Visualization using Python API such as Geopandas could have been made.
	If permitted, I can make animated Dashboard in Tableau(as its propertiary, So I havn’t used)
	Gradient Boosting method could have been used if were dealing better data and more models were being made.

