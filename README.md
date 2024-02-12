
# Case Study: Chain of Departmental Stores Analysis

# Business Problem
The company’s CEO and stakeholders are excited to know about their sales across various departments and stores. They want to know sales across each store and compare current year sales to the last year sales. The big plan is to develop a dashboard and see self-explanatory insights. There was no data pipeline/warehouse available as such. Weekly data is extracted using a data tool connected to the POS at every store. Every week the Senior Assistant extracts the number of files and demands to update the dashboard and then send it to the CEO via a link or otherwise.  

# Dataset Overview
Fortunately, the company possesses a valuable asset: a dataset with information about weekly sales data across various stores and departments.

•	**Department:** A dataset      
comprising information about departments.

•	**Store:** A dataset having information about stores and store managers. Especially, helpful to determine top performing managers.

•	**Weekly Sales Data:** A dataset having information about weekly sales from year 2011 to 2012.

Link to the Dataset: Data

# Objective
We want to take a close look at the data we already have, figure out the trends for weekly sales around both years and see YTD (Year to Date) comparison for each store and department across each week. We’ll also look at top performing stores and departments and give commission to the top 5 performing store’s manager. Let’s dig into the information and see the weekly sales trend.

# Case Study Roadmap
Here’s the framework I’ve created for conducting this case study.

1.	**Research:** Understand the company’s nature and objectives to determine how the analysis can benefit them.

2.	**Business Problem:** Identify the specific business problem that the company is facing and that data analysis can help solve.

3.	**Scenario Setup:** Construct a scenario that aligns with the chosen business problem for analysis.

4.	**Ask Questions:** Develop relevant questions based on the chosen business problem and scenario to guide the analysis.

5.	**How to Proceed:** Outline a preliminary plan or blueprint for the analysis, detailing the steps to be taken for success.

6.	**Select the Right Tools:** Choose appropriate tools, such as Power BI, needed for the analysis based on the scale of business and sales.

7.	**Explore the Dataset:** Familiarize yourself with the basics of the dataset, gaining an understanding of its structure and content.

8.	**Analysis:** Perform the analysis as per the plan, using the selected tools and addressing the questions formulated earlier.

# Data Cleaning/Preprocessing/Transformation

1.	**Handling Missing Values:** Checked the dataset for any missing values using BI’s view tab. The datasets didn’t have any missing values for any columns.

2.	**Duplicate Data Handling:** There were no duplicate rows in the dataset.

3.	**Handling Data Type Inconsistencies:** Transformed the data type of date column to date datatype using ‘Power Query Editor’.

4.	**Normalization:** Employed a separate date dimension table using M-query to reduce the redundancy of ‘Sales’ data. 

5.	**Sales Folder:** All weekly sales datasets were placed in a folder ‘Sales’. The ‘Sales’ folder was directly imported in Power BI.  Moreover, the upcoming weekly sales data can be added to the folder and BI can be refreshed to update the dashboard automatically.

# Data Modelling
**Star Schema**

Employed a data schema using star schema approach to establish relationship between different tables.

![App Screenshot](https://github.com/MuhammadTabishSami/Case-Study-Chain-of-Departmental-Stores-Analysis/blob/master/Data%20Model.jpg?raw=true)

**KPIs and Measures**

Employed calculated measures to create Key Performance Indicators (KPIs) showing total sales, YTD sales current year, YTD sales previous year, total commission for managers using Data Analysis Expressions (DAX) in Power BI.

1.	**DAX for Total Sales**
Total Sales = SUM('Factweekly_sales'[Weekly_Sales]) 

**Result:** The company’s total sales were ‘180.1M’.  

2.	**DAX for VS Previous Year**

vs YTD = [YTD Sales Current Year]/[YTD Sales Previous Year]

**Result:** The index ‘0.83’ showed decline in sales as compared to previous year. 

3.	**DAX for YTD Sales Current Year**

YTD Sales Current Year = 
CALCULATE(
    SUM('Factweekly_sales'[Weekly_Sales]), 
    FILTER(
        ALL(DimDate), 
        DimDate[Year] = MAX(DimDate[Year]) && 
        DimDate[Week Number] <= MAX(DimDate[Week Number])
    )
)

**Result:** It shows the total sales ‘81.5M’ till current week of the present year.

4.	**DAX for YTD Sales Previous Year**

YTD Sales Previous Year = 
CALCULATE(
    SUM('Factweekly_sales'[Weekly_Sales]), 
    FILTER(
        ALL(DimDate),
        DimDate[Year] = MAX(DimDate[Year]) - 1 && 
        DimDate[Week Number] <= MAX(DimDate[Week Number])
    )
)

**Result:** It shows the total sales ‘98.61M’ till current week of previous year.

 
5.	**DAX for Total Commission**

Total Commissiom = SUM('Factweekly_sales'[Commision])

**Result:** The total commission calculated to show top 5 manager’s commission.

# Data Analysis
**Sales Performance over Time**

The sales performance over time shows the trend of sales over time. It demonstrates how well the weekly sales are performing from year to year. There are noticeable peaks in sales at certain times of the year, which could correspond to holiday seasons or promotional events. The sales pattern indicates the impact of seasonality on sales. Sales tend to increase towards the end of the year, likely due to the holiday shopping season surrounding Black Friday, Christmas, and New Year’s Eve.

**Result:** Weekly sales for present year is performing well as compared to the previous year. The previous year’s trend indicates the sales boost at the end of present year.  

**Top Performing Stores and Departments**

The top performing stores and departments show the top performers based on their total sales to the current week.  

**Result:** The high-performance key metrics such as location, store size, customer demographics, product assortment and marketing campaigns can be adopted to optimize sales across the underperformance stores.

**Top 5 Stores Manager and their Commission**

This indicates the top 5 performing managers and their commissions to the current week.

**Result:** The managers performance sets benchmark for other store managers, boosting morale for these managers and encouraging competitive spirit among managers.

# Questions. 

**Which tool is best for weekly sales dashboard development ? Recommend tool on the basis of business scale and sales.**

As the organization is well aware of the Microsoft ecosystem and requires advanced BI capabilities, robust security, and scalability, Power BI is the recommended choice. It’s particularly suited for more comprehensive dashboards with deep insights into sales performance across different stores and departments. It will cater to scalability of the large datasets as business grows, offering BI capabilities, and security features.   

**How long it takes to refresh the data? Make a case to convince CEO for org data?**

The data refresh process takes from few minutes to an hour depending upon the data cleaning and transformation. Employing the Extract, Transform, Load (ETL) tools can automate the weekly sales data extraction from POS system and its loading to the dashboard tool. Moving towards data warehouse will improve data management, scalability and analysis capabilities.

**What Top 10 stores and departments are based on? Also, think about the bottom performing stores/departments?**

The top 10 stores and departments indicates the key driving factors such as location, size, customer demographics, consumer demand, and effective management to boost the weekly sales.

The bottom performing stores and departments are performing low due to range of factors including store size, location disadvantage, less effective management, and high local competition.

The performance insights from top performers should be distributed among bottom performers to optimize their sales and business growth.

# Report/Key Insights

1.	Overall sales are 4.45bn.
2.	Sales performance over year shows increase in sales growth as compared to previous year.
3.	Sales trend shows the sales boost at the end of present year.
4.	The best time to adopt marketing strategies to drive the sales is:

a.	November to December

b.	Holiday Shopping seasons

c.	Black Friday

d.	Christmas

e.	New Year Eve’s

# Recommendations
1. For Below performing stores and departments, deploy key drivers of sales from top performers such as location, store size, stock availability, customer demographics, product assortment, shop layout, and marketing strategies to boost sales across the underperforming stores and departments.

2. The marketing strategies such as holiday theme deployment will increase customer engagement, resulting in sales growth.
