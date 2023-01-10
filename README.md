# Exploratory-analysis-of-international-brewery-brands
Exploratory analysis of international brewery brands in Anglophones and Francophone countries in Africa between 2017 and 2019 using SQL.
![image](https://nairametrics.com/wp-content/uploads/2022/05/International-Breweries.png)


### PROJECT DESCRIPTION

The most common, popular alcoholic beverage consumed by Africans is Beer. Non-acoholic malt drinks are also very common beverages consumed by Africans and are produced in the same way as Beer except that it is not fermented. These brands represents a very substantial percentage of the total revenue of breweries. I made this analysis using 5 different Beer brands and 2 different Malt brands that are consumed in West Africa. 
In this project, I carried out a profit analysis, brand analysis and country analysis to know what brand has the highest sale, generated the most profit and what country consumed the most beverage.




### ABOUT THE DATASET
This dataset (*International_Breweries.csv*) contains the data about international brewery brands consumed in 5 Anglophone and Francophone countries in west africa which includes Nigeria, Ghana, Togo, Benin and Senegal between 2017 and 2019.

**The columns contained in the dataset are :**
1. Sales rep
2. Sales ID
3. Emails
4. Brands
5. Countries
6. Region
7. Months
8. Years
9. Quantity
10. Cost
11. Unit price
12. Profit
13. Plant cost

### Analysis Using SQL Queries (*file: sql analysis.sql*).


```
Create database Breweries;

Create Table International_breweries(
Sales_id int,
Sales_rep Varchar (255),
Emails varchar(255),
Brands varchar(255),
Plant_cost decimal(10,2),
Unit_price decimal(10,2),
Quantity decimal(10,2),
Cost decimal(10,2),
Profit decimal(10,2),
Countries varchar (255),
Region varchar(255),
Months varchar(255),
Years int,
Primary key (Sales_id)
);

select * from international_breweries;

select sum(Profit) from International_breweries;
 
 select sum(profit) AS Anglophone_profit from International_breweries
 where countries IN ('Nigeria','Ghana');
 
 select sum(profit) as Francophone_profit from International_breweries
 where countries in ('Togo','Benin','Senegal');

select countries, max(profit) as highest_profit_generated
from International_breweries where years =2019
group by countries
order by max(profit) DESC
limit 1;

 select years, max(profit) as highest_profit
from International_breweries 
group by years
order by max(profit) DESC
limit 1;

select months, min(profit) as least_profit
from International_breweries
group by months
order by min(profit)DESC
limit 1;

select min(profit) from International_breweries
where Months = 'December' and Years = '2018';

select months, Round(sum(profit) * 0.01) as Profit_Percentage
from International_breweries
where years = 2019
group by months
order by percentage;

select Brands, max(profit)as highest_profit
from International_breweries where Countries = 'Senegal'
group by brands
order by max(profit)desc
limit 1;

--Section B: Brand Analysis
/*1.Within the last two years, the brand manager wants to know the top three brands
consumed in the francophone countries*/ 
select brands, sum(Quantity)
from International_breweries 
where years in (2019, 2018)and countries in ('Togo','Benin','Senegal')
group by brands
order by sum(Quantity) DESC
limit 3;

select brands, sum(Quantity)
from International_breweries 
where countries = 'Ghana'
group by brands
order by sum(Quantity) DESC
limit 2;

select brands, sum(quantity) as quantity, sum(profit) as profit
from International_breweries where years in (2017, 2018,2019) and 
countries = 'Nigeria'
group by brands;

select brands, sum(quantity) 
from International_breweries where years in (2018,2019)
and countries in ('Ghana','Nigeria') and 
brands in ('Beta Malt','Grand Malt')
group by brands;

select brands, sum(quantity) as quantity_sold
from International_breweries
where years = 2019 and countries = 'Nigeria'
group by brands
order by sum(quantity) desc;

select brands, sum(quantity) as quantity_sold
from International_breweries
where region = 'Southsouth' and countries = 'Nigeria'
group by brands
order by sum(quantity)desc;

select brands, sum(quantity) as Total_beer_consumed
from International_breweries
where countries = 'Nigeria' and 
brands in ('Eagle Lager', 'Trophy', 'Hero', 'Budweiser', 'Castle Lite')
group by brands
order by sum(quantity)desc;

select brands, sum(quantity)as Budweiser_consumption
from International_breweries
where countries = 'Nigeria' and brands = 'Budweiser'
group by brands
order by sum(quantity);

select region, sum(quantity)
from International_breweries
where countries = 'Nigeria' and years = 2019 and brands = 'Budweiser'
group by region;

Select countries,sum(quantity)as amount_consumed
from International_breweries
where brands in ('Eagle Lager', 'Trophy', 'Hero', 'Budweiser', 'Castle Lite')
group by countries
order by sum(quantity);

select Sales_rep, sum(quantity) 
from International_breweries
where brands = 'Budweiser' and countries = 'Senegal'
group by Sales_rep
order by sum(quantity)DESC
limit 1;

select countries, sum(profit) as highest_profit
from International_breweries
where years = 2019 and months in ('October','November','December')
group by countries
order by sum(profit) desc
limit 1;

```

