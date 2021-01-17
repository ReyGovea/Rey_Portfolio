# [Project 1: Summary Reports: Objectives](https://github.com/ReyGovea/SAS-Projects)
* Creating a sales report from the Orion_fact data set 
* Demonstrating date formatting, subsetting, macrovariable use, tabulation 

## Catelog and Internet Sales 

Wanting to inquire on the range of the two different sales types. We can conclude that catelog sales are more prfitable than the companies internet sales. With a maximum sales value of roughly $1937 and a mean of approximately $200 which exceeds the internets sales values. 

![](https://github.com/ReyGovea/SAS-Projects/blob/main/Portfolio%20Images/Screen%20Shot%202020-12-15%20at%203.53.04%20PM.png?raw=true)

## Inserting Current Times into Titles 

Assigning macrovariable to the table title to streamline time and date of report. This means that as future sales are added to the companies database, the code will easily adapt represent the change in time. 

![](https://github.com/ReyGovea/SAS-Projects/blob/main/Portfolio%20Images/Screen%20Shot%202020-12-15%20at%204.04.15%20PM.png?raw=true "Date Format")

## Overriding Existing Labels and Formats 

The origional report for the customers from Turkey has both large variable names as well as a ddmmmyyyy date format. In order to streamline the appearence of the report, applying a label change and the date format allows for easy reading of the customer information. 

![](https://github.com/ReyGovea/SAS-Projects/blob/main/Portfolio%20Images/Screen%20Shot%202020-12-15%20at%204.24.13%20PM.png?raw=true "Turkey Customers")

## Subsetting and Grouping 

The data set is organized by order_ID numbers that provide order dates, delivery dates, and order type. I want to organize the data by creating a new data set that is first set by order type in ascending sequence and then order date in descending sequence. Now that the origional data is organized, I want to subset to print BY order type for orders placed in the first 4 months of 2005 and those that have been delivered exactly 2 days after the order was placed. 

![](https://github.com/ReyGovea/SAS-Projects/blob/main/Portfolio%20Images/Screen%20Shot%202020-12-16%20at%201.57.00%20PM.png?raw=true "Orion Star Sales Details")
![](https://github.com/ReyGovea/SAS-Projects/blob/main/Portfolio%20Images/Screen%20Shot%202020-12-16%20at%201.57.07%20PM.png?raw=true "Orion star ... Filters")

## Tabular Report 

Wanting to create a tabulation of the mean customer age for the group name and gender of the customer. Assigning Customer Group and Customer Gender as classification variables. This tabular report highlights that both older men and woman tend to be internet/catelog customers while both younger men and women tend to be Orion Club Gold Members. However, for normal orion members, young females tend to subscribe while older men on averege tend to apply. This information could be important to highlighting who the company should be advertising to as well as curtailing its services for. 

![](https://github.com/ReyGovea/SAS-Projects/blob/main/Portfolio%20Images/Screen%20Shot%202020-12-16%20at%202.17.04%20PM.png?raw=true "Tabular Report")

# [Project 2: Seoul Bike Rental Regression Analysis: Summary](https://github.com/ReyGovea/R_Projects-) 
* Collection of weather data that corresponds to bike rental counts in Seoul from [UCI Machine Learning Repository](https://archive.ics.uci.edu/ml/datasets/Seoul+Bike+Sharing+Demand )
* Attempting to measure the relationship between weather conditions and the expected bike rental count 
* considering the implications for bike rental companies as they address how weather impacts their demand 
* Utilization of model selection, model comparison, Multiple Linear Regression (MLR), Zero Inflated Negative Binomial (ZINB) regression
* 9 numeric independent variables used and used rental bike count as the response variable (n=8760)

## Model Selection and Multicolinearity

The full model considered the variables hour, temperature, humidity, windspeed, visibility, dew point temperature, solar ratdiation, rainfall and snowfall. In order to select the best fitting model, stepwise selection was applied to the data with an AIC standard and output the following model...

expected(RentedBikeCount)=β0+β1(Hour)+β2(Temperature)+β3(Humidity)+β7(SolarRadiation)+β8(Rainfall)+ϵ

... In order to apply a linear model to the data, the models assume that all independent variables are independant from another. In oder to verify that the new model does not defy this assumption the Variance Inflation Factor was used to measure independance. 

![](https://github.com/ReyGovea/R_Projects-/blob/main/Portfolio%20Work/Images/Screen%20Shot%202020-12-17%20at%202.45.37%20PM.png?raw=true "VIF")

The Assumption that all of the variables in the model are independent is validated by all VIF values in the model being less than 5. We can now continue to assess the other assumptions in the model to see if a MLR model is a good fit for the data. 

## Multiple Linear Regression 

Now that we know there is no multicolinearity in the model, it is important to look at the residuals of the model to diagnose issues with non-linearity, non-constant variance, and extreme outliers. Violation of these conditions in the data would make a MLR model potentially a bad fit. 

![](https://github.com/ReyGovea/R_Projects-/blob/main/Portfolio%20Work/Images/Screen%20Shot%202020-12-17%20at%202.59.51%20PM.png?raw=true "MLR Resid.")

There are a few conclusions that can be drawn from the residual plots: the data is non-linear and skewed right, there is a bottom floor to the values and a residuals shape that indicates heteroscedasticity, and there are outliers in the data but none that indicate significant leverage. 

### Initial Change: Power Transformation

When a data set is non-normal and there are problems with non-constant variance a power-transformation is useful tool in adjusting for the violation in model assumptions. Normally, a good way to estimate a good lambda value is through the box-cox method. However, with this data set holding a lot of zero values, the log based analysis results in undefined values. In this case, the Yeo-Johnson method is being used to account for the zero values in the data. 

![](https://github.com/ReyGovea/R_Projects-/blob/main/Portfolio%20Work/Images/Screen%20Shot%202020-12-17%20at%203.22.11%20PM.png?raw=true "Yeo-Johnson")
![](https://github.com/ReyGovea/R_Projects-/blob/main/Portfolio%20Work/Images/Screen%20Shot%202020-12-17%20at%203.22.23%20PM.png?raw=true "Transformed MLR Resid.")

We can see that the Yeo-Johnson method suggested a power transformation of roughlu lambda = 0.4 and the corresponding residuals for the transformed response variable. There seems to be a slight correction heteroscedasticity as random variance becomes better. However, observation 3998 has become a significantly leveraged outlier and the normal Q-Q plot indicates that the model is still not normal. 

## Zero Inflated Negative Binomial Model 

A poisson regression model would initially be considered for correcting the non-normality assumption violation in the model. The data is skewed right and follows a general poisson distribution. However, a poisson regression model assumes that the mean and variance in the distribution is the same. The data has a mean of roughly 705 and variance of 416,021. This vast difference violates the model assumption of poisson regression. A ZINB model would not care about the equal variance and mean assumption, heteroscedasticity, and would not be constrained by normality. With 295 zero values in the data, the zero inflation is to correct for the large zero values that a general negative binomial model would not account for. 

![](https://github.com/ReyGovea/R_Projects-/blob/main/Portfolio%20Work/Images/Screen%20Shot%202020-12-17%20at%203.44.20%20PM.png?raw=true "ZINB Model Output" )

When we run the zero inflated negative binomial model we can see that with a residual range of the data is from [-1.3887, 20.1355] and there is an IQR of 1.835. we can infer that there are some outliers present in the distribution, this may be of some concern and should be considered moving forward. With the zero inflated model, we can see that Temperature is the only significant variable with a p-value of 2.66e-05. This indicates that there is a statistically significant relationship between the Temperature variable and the log expected Rental Bike Count. We can interpret the coefficient to be that for every one unit change in temperature, the difference in the log of the expected Rental Bike Count is expected to change by 0.025176, given that the other predictors are held constant.

## Model Comparison

One way to compare the models is to look at the AIC values of each model and compare them, with lower AIC values indicating a better fit. The AIC values are as follows 
* MLR = 132651
* ZINB = 124821.8

Considering that the assumptions with the ZINB model were not violated and that the AIC values indicate a better fit to the population relationships, it seems like it is a better fitting model to predict the population relationships. 


## Discussion/Conclusion

The bike rental industry in Seoul has largely grown in the past decade as technology has made phone app access to bikes highly accessible. This methedology provides the best General Linear Model (GLM) to predict weather impacts on of weather on bike rental counts. However, machine learning techniques would potentially provide better estimates on the populations relationship between weather conditions and the rental counts. 

The outcome of the ZINB model suggests that temperature is the statistically significant variable that impacts the change in bike rental counts. The implications for bike rental companies may include scheduling maintenence of bikes for extreme weather temperatures where demand for their product will be at its lowest point. This would maximize the supply of the product for high demand. Also, the company could look at temperature variations in the city and decide where to locate their rental stations to accomidate regions that are associated with better weather conditions. In these ways, actionable descisions can be made to adjust to the impacts that weather has on the industry. 

# [Project 3: SQL Queries: Objectives](https://github.com/ReyGovea/SAS-Projects/blob/main/Code_%2002%20SQL%2C%20Basic%20Queries%20HW.sas.pdf)
* Utilize SQL coding in SAS terminal to extract and combine essential information from the Orion buisness tables
* Subsetting data to organize and highlight information 
* Creating variables 

## Subsetting data 

Taking the table of "Employee Payroll" from the Orion data base. Utilizing the select statement to subset the data into a table of four variables after printing the whole data set.
``` 
Proc SQL;
	SELECT *
		FROM orion.Employee_Payroll;
	SELECT Employee_ID, Employee_Gender, Marital_Status, Salary
		FROM orion.Employee_payroll;
Quit;
```
![](https://github.com/ReyGovea/SAS-Projects/blob/main/Portfolio%20Images/Screen%20Shot%202021-01-17%20at%204.53.43%20PM.png?raw=true "Orion payroll subset" )

## Creating a Calculated Variable

The employee payroll data set has a percentage of their employees slary that is applied to taxes. The tax rate is considered to be 1/3 of the salary. We want to create a calculated variable called tax that is a calculation of the expected tax amount.

```
Proc SQL;
	SELECT Employee_ID, Employee_Gender, Marital_Status, Salary, Salary*.333 AS Tax
		FROM orion.Employee_payroll; 
Quit;
```
![](https://github.com/ReyGovea/SAS-Projects/blob/main/Portfolio%20Images/Screen%20Shot%202021-01-17%20at%205.03.00%20PM.png?raw=true "Tax Calculation")

## Conditional Processing 

The Orion staff table has given variables such as the employee_id, Job_titles and Salary of their workers. I want to create a variable that assigns three salary ranges for Job_titles labeled "Low" "Medium" and "High". 

```
Proc SQL;

	SELECT Employee_ID, Salary,
			CASE scan(Job_title, -1, ' ') /*needing a space in the quote for program to notice more than one word*/
				WHEN "Manager" THEN "Manager"
				WHEN "Director" THEN "Director"
				WHEN "Officer" THEN "Executive"
				WHEN "President" THEN "Executive"
				ELSE "NA"
			END AS Level,
			
			CASE /*needing to include calculated level by the when statement for code to recognize non-existing data*/
				WHEN Calculated Level='Manager' AND Salary < 52000 THEN 'Low'
				WHEN Calculated Level='Manager' AND Salary ge 52000 AND Salary le 72000 THEN 'Medium'
				WHEN Calculated Level='Manager' AND Salary > 72000 THEN 'Large'
				
				WHEN Calculated Level='Director' AND Salary < 108000 THEN 'Low'
				WHEN Calculated Level='Director' AND Salary ge 108000 AND Salary le 135000 THEN 'Medium'
				WHEN Calculated Level='Director' AND Salary > 135000 THEN 'High'
				
				WHEN Calculated Level='Executive' AND Salary < 240000 THEN 'Low'
				WHEN Calculated Level='Executive' AND Salary ge 240000 AND Salary le 300000 THEN 'Medium'
				WHEN Calculated Level='Executive' AND Salary > 300000 THEN'High'
			END AS Salary_Range
	FROM orion.Staff
	WHERE Calculated Level NE 'NA'; /*This statement should make including 'NA' in 2nd case statement not needed*/
Quit;
proc print data=orion.staff; run;

```
![](https://github.com/ReyGovea/SAS-Projects/blob/main/Portfolio%20Images/Screen%20Shot%202021-01-17%20at%205.09.59%20PM.png?raw=true "Salary Ranges")

## Eliminating Duplicates 

Orion holds tables of their employee's addresses. The table that holds these addresses has duplicates of the cities that their employees reside. I want to solve for what cities the employee's reside in without duplicates. 

```
title 'Cities Where Employees Live';
Proc SQL;
	Describe Table Orion.Employee_Addresses; /*Looking at variable names and type in table*/
	SELECT UNIQUE(City)
		FROM Orion.Employee_Addresses;
Quit;
title;
```

![](https://github.com/ReyGovea/SAS-Projects/blob/main/Portfolio%20Images/Screen%20Shot%202021-01-17%20at%205.16.55%20PM.png?raw=true "Employee cities")

## Limiting Calculated Totals

Creating a calculated total of the sum total of employee donations per quarter. I want to see if the total donations of the employee's are greater than $90. 

```
Proc SQL;
	Describe Table orion.Employee_donations; /*looking at table attributes*/
	SELECT Employee_ID, Recipients, qtr1+qtr2+qtr3+qtr4 AS Total
	FROM orion.Employee_donations 
		WHERE CALCULATED total >90;
Quit;
```
![](https://github.com/ReyGovea/SAS-Projects/blob/main/Portfolio%20Images/Screen%20Shot%202021-01-17%20at%205.21.48%20PM.png?raw=true "Employee donations > $90")


















