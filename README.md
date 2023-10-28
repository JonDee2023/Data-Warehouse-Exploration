# Data-Warehouse-Exploration
My work with Azure Synapse Analytics dedicated SQL pool (as a data warehouse)

Azure Synapse Analytics is built on a scalable set capabilities to support enterprise data warehousing; including file-based data analytics in a data lake as well as large-scale relational data warehouses and the data transfer and transformation pipelines used to load them. In this lab, I explored how to use a dedicated SQL pool in Azure Synapse Analytics to store and query data in a relational data warehouse.

An Azure subscription in which I have have administrative-level access was required.

The following link contains a full description of this exercise. 
https://microsoftlearning.github.io/DP-500-Azure-Data-Analyst/Instructions/labs/03-Explore-data-warehouse.html

# Clone github repo to create Azure Synapse Analytics workspace
rm -r dp500 -f
git clone https://github.com/MicrosoftLearning/DP-500-Azure-Data-Analyst dp500

# Provision dedicated SQL pool with data warehouse to be used for this lab
cd dp500/Allfiles/03
./setup.ps1

# SQL queries to analyze data in data warehouse

SELECT d.CalendarYear AS Year,
       SUM(i.SalesAmount) AS InternetSalesAmount
FROM FactInternetSales AS i
JOIN DimDate AS d ON i.OrderDateKey = d.DateKey
GROUP BY d.CalendarYear
ORDER BY Year

SELECT d.CalendarYear AS Year,
       d.MonthNumberOfYear AS Month,
       SUM(i.SalesAmount) AS InternetSalesAmount
FROM FactInternetSales AS i
JOIN DimDate AS d ON i.OrderDateKey = d.DateKey
GROUP BY d.CalendarYear, d.MonthNumberOfYear
ORDER BY Year, Month


SELECT d.CalendarYear AS Year, 
       g.EnglishCountryRegionName AS Region,
       SUM(i.SalesAmount) AS InternetSalesAmount
FROM FactInternetSales AS i
JOIN DimDate AS d ON i.OrderDateKey = d.DateKey
JOIN DimCustomer AS c ON i.CustomerKey = c.CustomerKey
JOIN DimGeography AS g ON c.GeographyKey = g.GeographyKey
GROUP BY d.CalendarYear, g.EnglishCountryRegionName
ORDER BY Year, Region
![Analyze Internet Sales](https://github.com/JonDee2023/Data-Warehouse-Exploration/assets/123139569/caf3ea07-4fec-4a54-b36e-0532a305311e)
![Analyze Internet Sales (1)](https://github.com/JonDee2023/Data-Warehouse-Exploration/assets/123139569/0a5d5a77-0023-480c-84ea-e845a4527bb8)
![Analyze Internet Sales](https://github.com/JonDee2023/Data-Warehouse-Exploration/assets/123139569/bd43bc30-f9cb-4ce9-aafb-e4aea6a8ea7d)
![Analyze Internet Sales (2)](https://github.com/JonDee2023/Data-Warehouse-Exploration/assets/123139569/adfd1701-1705-49be-a12b-03d52eaa495b)
