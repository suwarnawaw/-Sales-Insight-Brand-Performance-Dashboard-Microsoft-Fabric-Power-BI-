📊 Sales Insight & Brand Performance Dashboard (Microsoft Fabric + Power BI)
📌 Project Overview

This project demonstrates an end-to-end analytics pipeline built using Microsoft Fabric and Power BI to analyze sales performance across brands, categories, and time.The solution ingests raw data from GitHub-hosted Excel files, processes it using Microsoft Fabric Data Pipelines, and builds a semantic model and interactive Power BI dashboard for business insights.
The architecture follows the Medallion Data Architecture (Bronze → Silver → Gold) which ensures scalable, maintainable, and high-performance analytics.

🏗 Architecture Overview
Medallion Architecture
The project follows the Medallion Architecture pattern, commonly used in modern data platforms such as Microsoft Fabric, Databricks, and Azure Data Lake.

                +----------------------+
                |     Data Source      |
                |  GitHub Excel Files  |
                +----------+-----------+
                           |
                           v
                +----------------------+
                |   BRONZE LAYER       |
                | Raw Data Ingestion   |
                | Fabric SQL Database  |
                +----------+-----------+
                           |
                           v
                +----------------------+
                |   SILVER LAYER       |
                | Data Cleaning        |
                | Data Modeling        |
                | Relationships        |
                +----------+-----------+
                           |
                           v
                +----------------------+
                |    GOLD LAYER        |
                | Business Metrics     |
                | Semantic Model       |
                | Power BI Dashboard   |
                +----------------------+
🥉 Bronze Layer – Data Ingestion

The Bronze layer contains raw ingested data from the source.
Data Source

The data is sourced from Excel files hosted on GitHub.
Two datasets are ingested:
Item Table
Sales Table

Ingestion Method
Table	Method	Tool
Item	Copy Job	Microsoft Fabric
Sales	Copy Activity	Fabric Data Pipeline

Copy Job – Item Table
The Item table is ingested using Fabric Copy Job.
    Features used:
      HTTP connection to GitHub
      Data type validation
      Full load / incremental load capability
Steps:
    Create Copy Job
    Select HTTP source
    Connect to GitHub Excel file
    Validate schema and data types
    Run job to load data
The table is then stored in Fabric SQL Database.

Copy Activity – Sales Table
The Sales table is ingested using Fabric Data Pipeline Copy Activity.
Steps:
    Create a new Data Pipeline
    Add Copy Activity
    Configure HTTP source from GitHub
    Validate schema
    Load into Fabric SQL Database
The Sales data is now available for analytics.

🥈 Silver Layer – Data Modeling
The Silver layer prepares the data for analytics.
      This layer includes:
          Data cleaning
          Relationship creation
          Date table creation
          Semantic model preparation
          
Data Model
  Tables used:
      Table	Description
      Sales	Transactional sales data
      Item	Product and category data
      Calendar Date dimension

Relationships
The following relationships are created:
    Item[ItemId] 1 ----- * Sales[ItemId]
    Date[Date]   1 ----- * Sales[SalesDate]


This enables:
Category analysis
Brand performance tracking
Time-based analysis
Calendar Table
    A Calendar table is created using DAX.

Example:
    Calendar =
        CALENDAR ( DATE(2018,1,1), DATE(2025,12,31) )
The table is then marked as a Date table to support time intelligence functions.

🥇 Gold Layer – Business Analytics
The Gold layer contains business-ready data models used by Power BI reports.
A Semantic Model is created from the Fabric SQL Analytics Endpoint.

This model supports:
    KPI calculations
    Business metrics
    Analytical queries

📊 Power BI Dashboard
The Power BI report provides interactive analysis of sales performance.
Key Metrics
    The dashboard tracks the following KPIs:
      Net Profit
      Gross Amount
      COGS
      Discount Amount
      Total Orders
      Total Quantity Sold

📈 Dashboard Insights
Brand Performance
Shows Top 5 Brands by Quantity Sold.
Helps identify:
Best selling brands
High demand products
Category Profitability
Displays Net Profit by Category.
Used to identify high margin categories.
Order Trends
A quarterly chart showing Total Orders over time.
  Helps detect:
    Demand trends
    Sales decline patterns
    Seasonal spikes
    Month over Month (MoM) Sales
        Shows Previous Month Sales vs Current Month Sales and the MoM growth percentage.
        This helps track:
            Business growth
            Revenue decline periods
            Sub-Category Performance
            Displays Top Sub-Categories by Net Profit.
            Helps optimize product strategy.

📊 Example DAX Measures
Total Orders
      Total Orders = COUNT(Sales[OrderID])
Gross Amount
      Gross Amount = SUM(Sales[GrossAmount])
Net Profit
      Net Profit =
          SUM(Sales[GrossAmount])- SUM(Sales[COGS])- SUM(Sales[Discount])
MoM Growth
      MoM % = DIVIDE(
              [CurrentMonthSales] - [PrevMonthSales],
              [PrevMonthSales]
            )

📷 Dashboard Preview
Sales Brand Performance Dashboard


Performance Analysis Dashboard


🎯 Business Use Cases
This dashboard can be used by:
Sales Teams
Product Managers
Category Managers
Executives

Business Analysts
  To support decisions such as:
      Product strategy
      Brand optimization
      Demand forecasting
      Revenue growth monitoring

🚀 Key Skills Demonstrated
Microsoft Fabric
Data Pipelines
Copy Jobs
Medallion Architecture
Data Modeling
Power BI Dashboard Development
DAX Measures
Time Intelligence

⭐ Future Enhancements
Planned improvements include:
Real-time streaming data
Customer segmentation analysis
Predictive sales forecasting
Row-Level Security (RLS)
Microsoft Fabric Lakehouse integration

📬 Connect With Me - If you are interested in Power BI, Data Analytics, or Business Intelligence solutions, feel free to connect. suwarna.w@gmail.com https://www.linkedin.com/in/suwarnamala-wawhal 
