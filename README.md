# Business-Intelligence-Final-Project

## 1\. Project Title

Retail Sales Performance Analytics - End Semester Exam Project

## 2\. Student Information

**Name:** Lavender Nchagwa Mathias  
**Admission Number:** 669647

## 3\. Course Information

**Course Code:** DSA 3050A – Business Intelligence & Data Visualization  
**Class:** SS 2026

## 4\. Project Overview

This project presents an end-to-end Business Intelligence solution built in Power BI. The workflow encompasses data acquisition of raw transactional data, extensive ETL (Extract, Transform, Load) processes in Power Query, relational data modeling (Star Schema), advanced DAX metric development, and the design of an interactive 3-page executive dashboard to extract data-driven recommendations.

## 5\. Problem Statement

The objective is to design a BI solution that identifies key sales drivers across various product categories and customer demographics. Because the raw transactional data suffers from systemic entry errors, missing values, and inconsistencies, a robust data cleaning pipeline must be established to ensure stakeholders make decisions based on accurate and reliable performance metrics.

## 6\. Dataset Description

  * **Source:** Kaggle - [Retail Store Sales: Dirty for Data Cleaning](https://www.kaggle.com/datasets/ahmedmohamed2003/retail-store-sales-dirty-for-data-cleaning)
  * **Structure:** A single flat `.csv` file containing 12,575 transactional records (exceeding the 9,000-row requirement).
  * **Characteristics:** Contains a mix of categorical and numerical variables (Quantity, Total\_Amount, Category, Date). The dataset is intentionally "dirty," featuring nulls, missing price metrics, and formatting errors, providing the complexity needed for advanced transformation.

## 7\. Tools Used

  * **Power BI Desktop:** For Data Modeling, DAX calculations, and Dashboard Visualization.
  * **Power Query:** For data cleaning, transformation, and query management.

## 8\. Steps Followed

1.  **Data Acquisition:** Imported the raw 12,575-row dataset into Power BI.
2.  **Data Cleaning (Power Query):** Replaced missing values with 0, removed duplicates, standardized date formats, and corrected data types (e.g., converting financial columns to Fixed Decimal Number).
3.  **Data Transformation:** Extracted date components (Year, Month) and utilized M-code to engineer conditional columns and impute missing values.
4.  **Data Modeling:** Normalized the flat file into a Star Schema, creating one central `Fact_Sales` table and five surrounding dimension tables (`Dim_Product`, `Dim_Location`, `Dim_Payment`, `Dim_Customer`, `Dim_Date`).
5.  **DAX Development:** Authored calculated columns and measures to establish core KPIs and time-intelligence metrics.
6.  **Dashboard Design:** Built an interactive, 3-page report emphasizing a summary-to-detail analytical flow.

## 9\. Dashboard Features

  * **Design Philosophy:** Summary-to-Detail layout with a consistent color palette and clear typography.
  * **Page 1: Executive Summary:** High-level KPI cards and trend analysis charts.
  * **Page 2: Detailed Analysis:** Granular drill-down capabilities, matrix visuals, and a Decomposition Tree for operational exploration.
  * **Page 3: Insights and Performance Monitoring:** AI-driven Anomaly Detection and Time Intelligence analysis.
  * **Interactivity:** Full cross-filtering enabled across visuals, supported by global Location and Year slicers.

## 10\. Key DAX Measures & Calculated Columns

**Calculated Columns:**

  * `Total Cost`: `Fact_Sales[Quantity] * RELATED(Dim_Product[Price Per Unit])`
  * `Is High Value Transaction`: `IF(Fact_Sales[Total Spent] > 500, "High Value", "Standard")`

**DAX Measures:**

  * `Total Revenue`: `SUM(Fact_Sales[Total Spent])`
  * `Average Order Value`: `AVERAGE(Fact_Sales[Total Spent])`
  * `Total Transactions`: `COUNTROWS(Fact_Sales)`
  * `Unique Customers`: `DISTINCTCOUNT(Fact_Sales[Customer ID])`
  * `Total Quantity Sold`: `SUM(Fact_Sales[Quantity])`
  * `YTD Revenue`: `TOTALYTD([Total Revenue], Dim_Date[Transaction Date])`
  * `Previous Month Revenue`: `CALCULATE([Total Revenue], DATEADD(Dim_Date[Transaction Date], -1, MONTH))`
  * `Revenue Growth %`: `DIVIDE([Total Revenue] - [Previous Month Revenue], [Previous Month Revenue], 0)`

## 11\. Key Insights

  * **High-Value Customer Concentration:** Over 60% of Total Revenue is driven by "High Value" transactions (\>500), despite them representing a smaller percentage of overall volume.
  * **Geographic Performance Variance:** Urban centers (e.g., Downtown) dominate in Average Order Value (AOV), while suburban locations lead in raw transaction volume.
  * **Seasonality and Revenue Contraction:** There is a recurring 5-8% revenue decline in Month 2 of each quarter.
  * **Category Dominance and Stagnation:** Electronics drives top-line revenue, but Clothing is the primary driver of store traffic and purchase frequency.
  * **Discount Efficiency Gap:** Deep discounts are frequently applied to high-volume items with natural demand, unnecessarily sacrificing Gross Profit margins.

## 12\. Challenges Encountered

  * **Missing Price Imputation:** The raw data contained missing unit prices. This was resolved by engineering a custom M-code conditional column (`if [Price_per_Item] = null then [Total_Amount] / [Quantity] else [Price_per_Item]`) to ensure accurate financial aggregation.
  * **Star Schema Normalization:** Transforming a single, flat CSV file into a relational model required strict deduplication across descriptive fields to successfully establish the required $1:*$ cardinality and single cross-filter direction between the Dimension tables and the Fact table.

## 13\. Conclusion

This project successfully transformed a high-volume, error-prone dataset into a reliable analytical asset. By applying rigorous data hygiene, an optimized Star Schema, and strategic DAX logic, the resulting interactive dashboard uncovers actionable realities. The insights derived from AI-driven cross-filtering provide stakeholders with fact-based pathways to launch targeted loyalty programs, optimize regional inventory, and restructure discount strategies to protect profit margins.