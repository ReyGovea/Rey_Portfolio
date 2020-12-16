# [Project 1: Summary Reports: Objectives](https://github.com/ReyGovea/SAS-Projects)
* Creating a sales report from the Orion_fact data set 
* Demonstrating date formatting, subsetting, macrovariable use, tabulation 

## Catelog and Internet Sales 

Wanting to inquire on the range of the two different sales types. We can conclude that catelog sales are more prfitable than the companies internet sales. With a maximum sales value of roughly $1937 and a mean of approximately $200 which exceeds the internets sales values. 

![](https://github.com/ReyGovea/SAS-Projects/blob/main/Portfolio%20Images/Screen%20Shot%202020-12-15%20at%203.53.04%20PM.png)

## Inserting Current Times into Titles 

Assigning macrovariable to the table title to streamline time and date of report. This means that as future sales are added to the companies database, the code will easily adapt represent the change in time. 

![](https://github.com/ReyGovea/SAS-Projects/blob/main/Portfolio%20Images/Screen%20Shot%202020-12-15%20at%204.04.15%20PM.png)

## Overriding Existing Labels and Formats 

The origional report for the customers from Turkey has both large variable names as well as a ddmmmyyyy date format. In order to streamline the appearence of the report, applying a label change and the date format allows for easy reading of the customer information. 

![](https://github.com/ReyGovea/SAS-Projects/blob/main/Portfolio%20Images/Screen%20Shot%202020-12-15%20at%204.24.13%20PM.png)

## Subsetting and Grouping 

The data set is organized by order_ID numbers that provide order dates, delivery dates, and order type. I want to organize the data by creating a new data set that is first set by order type in ascending sequence and then order date in descending sequence. Now that the origional data is organized, I want to subset to print BY order type for orders placed in the first 4 months of 2005 and those that have been delivered exactly 2 days after the order was placed. 

![](https://github.com/ReyGovea/SAS-Projects/blob/main/Portfolio%20Images/Screen%20Shot%202020-12-16%20at%201.57.00%20PM.png)
![](https://github.com/ReyGovea/SAS-Projects/blob/main/Portfolio%20Images/Screen%20Shot%202020-12-16%20at%201.57.07%20PM.png)

## Tabular Report 

Wanting to create a tabulation of the mean customer age for the group name and gender of the customer. Assigning Customer Group and Customer Gender as classification variables. This tabular report highlights that both older men and woman tend to be internet/catelog customers while both younger men and women tend to be Orion Club Gold Members. However, for normal orion members, young females tend to subscribe while older men on averege tend to apply. This information could be important to highlighting who the company should be advertising to as well as curtailing its services for. 

![](https://github.com/ReyGovea/SAS-Projects/blob/main/STA4203_Assignment%203.sas)




