# Unicon Company.

## Project Overview

**Project Title**: Unicorn Companies Analysis Using SQL
- I worked with a real dataset of "unicorn" companies — I cleaned the data and used SQL to explore it.   
- I looked at industries, countries, valuations, funding, investors, and founding years.   
- I ran SQL queries to find patterns and trends.   
- I checked which industries and countries have the most unicorns.   
- I studied how funding and investors affect company growth.  

This project improved my SQL skills, helped me think like a business analyst, and taught me how to analyze real startup data. 
## Objectives.

**1.** **Set Up the Database.**     
**2.** **Data Cleaning.**      
**3.** **Perform Exploratory Data Analysis (EDA).**    
**4.** **Answer Business Questions Using SQL.**    

## Project Structure.

### 1. Database Setup:-
- **Put the unicorn companies data into that database**. `Unicorn_Details.`  
- **Table creation:-** Inside that database, create a table also called `Unicorn_Details.` to hold the customer data. The table will have columns for different pieces of information such as **:-** Company,	Valuation,	Date_Joined,	Industry,	City,	Country,	Continent,	Year_Founded,	Funding,	Select_Investors.  
 ```SQL
Create Database:-
CREATE DATABASE Unicon_details;
USE Unicon_details;

Create table:-
CREATE TABLE unicon_Details (
    company VARCHAR(150),
    valuation VARCHAR(50),
    date_joined DATE,
    industry VARCHAR(150),
    city VARCHAR(150),
    country VARCHAR(150),
    continent VARCHAR(150),
    year_founded INT,
    funding VARCHAR(150),
    select_investors TEXT
);
```
### 2. Data Cleaning:-
- Check for duplicate records.   
- Identify and handle missing values.   
- Standardize text fields such as industry and country names.   
- Validate data types for valuation, funding, and dates.

```SQL
finding duplicates:-

SELECT *
FROM unicorn_Details
WHERE company IN (
    SELECT company
    FROM unicorn_details
    GROUP BY company
    HAVING COUNT(*) > 1
)
ORDER BY company;

Deleting Duplidate:-

WITH delete_duplicate AS (
    SELECT *,
           ROW_NUMBER() OVER(PARTITION BY company ORDER BY company) AS company1
    FROM unicorn_details
)
DELETE FROM unicorn_details
WHERE company IN (
    SELECT
        company
    FROM delete_duplicate
    WHERE company1 > 1
);


```
### 3.Answer Business Questions Using SQL.
These SQL queries were written to answer important business questions about unicorn companies. It will help understand unicorn trends, compare countries and industries, and analyze company growth.
1. **Which are the Top 10 Most Valuable Unicorn Companies?**
```SQL
SELECT company,
       valuation
FROM unicorn_details
ORDER BY
    CAST(
        REPLACE(
            REPLACE(valuation,'$',''),
        'B','')
    AS DECIMAL(10,2)
    ) DESC
LIMIT 10;
```
2. **Which Country Has the Highest Number of Unicorn Companies?**
```SQL
SELECT country,
       COUNT(*) AS total_unicorns
FROM unicorn_details
GROUP BY country
ORDER BY total_unicorns DESC
LIMIT 1;
```
3. **Which City Has the Highest Number of Unicorn Companies?**
```SQL
SELECT city,
       COUNT(*) AS total_unicorns
FROM unicorn_details
GROUP BY city
ORDER BY total_unicorns DESC
LIMIT 1;
```
4. **Which Industry Has the Highest Number of Unicorn Companies?**
```SQL
SELECT industry,
       COUNT(*) AS total_unicorns
FROM unicorn_details
GROUP BY industry
ORDER BY total_unicorns DESC
LIMIT 1;
```
5. **Which Industries Show the Highest Growth Potential?**
```SQL 
SELECT industry,
       COUNT(*) AS total_unicorns
FROM unicorn_details
GROUP BY industry
ORDER BY total_unicorns DESC
LIMIT 10;
```

6. **Which Countries Have the Highest Average Valuation of Unicorn Companies?**
```SQL 
SELECT country,
       AVG(valuation) AS avg_valuation
FROM unicorn_details
GROUP BY country
ORDER BY avg_valuation DESC
LIMIT 10;
```
7. **Which Industries Attract the Largest Investments?**
```SQL
SELECT industry,
       COUNT(*) AS total_companies
FROM unicorn_details
GROUP BY industry
ORDER BY total_companies DESC;
```
8. **Which Continent Has the Highest Number of Unicorn Companies?**
```SQL 
SELECT continent,
       COUNT(*) AS total_unicorns
FROM unicorn_details
GROUP BY continent
ORDER BY total_unicorns DESC
LIMIT 1;
```
9. **Which Investor Has Invested in the Most Unicorn Companies?
```SQL 
SELECT select_investors,
       COUNT(*) AS total_investments
FROM unicorn_details
GROUP BY select_investors
ORDER BY total_investments DESC
LIMIT 10;
```
10. **What Are the Top 10 Oldest Unicorn Companies?**
```SQL
SELECT company,
       year_founded
FROM unicorn_details
ORDER BY year_founded ASC
LIMIT 10;
```
11. **How Many Unicorn Companies Were Founded in Each Year?**
```SQL 
SELECT year_founded,
       COUNT(*) AS total_companies
FROM unicorn_details
GROUP BY year_founded
ORDER BY year_founded;
```
12. **Which Companies Became Unicorns Most Recently?**
```SQL
SELECT company,
       date_joined
FROM unicorn_details
ORDER BY date_joined DESC
LIMIT 10;
```


## Conclusion

The Unicorn Companies SQL Project provides a comprehensive analysis of global billion-dollar startups. By leveraging SQL for data cleaning, exploration, and business intelligence, this project uncovers valuable insights into startup valuations, funding trends, industry performance, and geographic distribution. The findings can help investors, founders, and business leaders make data-driven decisions while showcasing practical SQL skills for a Data Analyst portfolio.
