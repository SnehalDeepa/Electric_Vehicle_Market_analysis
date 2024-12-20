# Electric_Vehicle_Market_analysis

## Business Statement

The Electric Vehicle Market Analysis project examines trends in EV adoption, manufacturer performance, and market dynamics using data-driven insights. It identifies key patterns in electric range, pricing, and geographic distribution to support stakeholders in making informed decisions. By highlighting opportunities and challenges, this analysis aligns with efforts to drive sustainability and innovation in the rapidly growing EV industry.

## Overview

The Electric Vehicle Market Analysis project is a comprehensive exploration of trends in the electric vehicle (EV) industry. Utilizing a robust dataset with 17 columns, this analysis dives into various aspects, including vehicle types, manufacturers, geographic distribution, and market dynamics. The project aims to uncover insights that can guide policymakers, manufacturers, and consumers toward informed decisions in the rapidly evolving EV landscape.This project leverages SQL and Python as primary tools for data analysis and visualization. Key libraries such as pandas, numpy, matplotlib, and seaborn are used to clean, analyze, and visualize the dataset effectively.

## Objective

The primary objective of this project is to analyze the electric vehicle market using data-driven methods to:
- Identify Trends: Discover trends in EV adoption across countries and regions.
- Analyze Manufacturers: Examine the market share and performance of key EV manufacturers.
- Ealuate Range & Pricing: Investigate relationships between electric range, MSRP, and vehicle type.
- Support Sustainability: Provide insights into how the EV market aligns with global sustainability goals.
- Showcase Skills: Demonstrate proficiency in SQL and Python for real-world data analysis projects.
- The findings of this analysis are presented through clear and engaging visualizations, making the insights accessible to a wide audience.

## Tool Used

- sql
- Power BI
- Python

## Data Used
- <a href="https://github.com/SnehalDeepa/Electric_Vehicle_Market_analysis/blob/main/compressed_data.csv.gz"<Dataset</a>

## SQL Schema

### STEP_1) DATA LOADING
### Import the dataset into your SQL environment and perform basic data inspection to verify column types, check for NULLs, and identify potential issues with data quality.

SELECT * FROM electric_vehicle_data;

### STEP_2) Answering Key Questions with SQL Queries
### Total vehicle count

```sql
SELECT COUNT(DOL_Vehicle_ID) AS TOTAL_vehicle
FROM electric_vehicle_data
```

### COUNT Battery electric vehicle

```sql
SELECT COUNT(Electric_Vehicle_Type) 
FROM electric_vehicle_data 
WHERE Electric_Vehicle_Type = 'Battery Electric Vehicle (BEV)';
```
### Percentage of BEV vehicle Type

```sql
SELECT 
    ROUND((COUNT(CASE WHEN Electric_Vehicle_Type = 'Battery Electric Vehicle (BEV)' THEN 1 END) * 100.0 / COUNT(DOL_Vehicle_ID)), 2) AS BEV_Percentage
FROM 
    electric_vehicle_data;
```

### COUNT Plug-in Battery electric vehicle (PHEV) 

```sql
SELECT COUNT(Electric_Vehicle_Type) 
FROM electric_vehicle_data 
WHERE Electric_Vehicle_Type = 'Plug-in Hybrid Electric Vehicle (PHEV)';
```

### Percentage of PHEV vehicle Type

```sql
SELECT 
    ROUND((COUNT(CASE WHEN Electric_Vehicle_Type = 'Plug-in Hybrid Electric Vehicle (PHEV)' THEN 1 END) * 100.0 / COUNT(DOL_Vehicle_ID)), 2) AS BEV_Percentage
FROM 
    electric_vehicle_data;
```

### EV Count by Country, State, and City

```sql
SELECT county, state, city, COUNT(DOL_Vehicle_ID) AS vehicle_count
FROM electric_vehicle_data
GROUP BY county, state, city
ORDER BY vehicle_count DESC;
```

### EV Distribution by Census Tract and Legislative District

```sql
SELECT _2020_Census_Tract, legislative_district, COUNT(DOL_Vehicle_ID) AS ev_count
FROM electric_vehicle_data
GROUP BY _2020_Census_Tract, legislative_district
ORDER BY ev_count DESC;
```

--STEP_3)Popular EV Manufacturers and Models
--Top Manufacturers by EV Count

SELECT Make, COUNT(DOL_Vehicle_ID) AS vehicle_count
FROM electric_vehicle_data
GROUP BY Make
ORDER BY vehicle_count DESC;

--Top Models by Region

SELECT county, Make, model, COUNT(DOL_Vehicle_ID) AS model_count
FROM electric_vehicle_data
GROUP BY county, Make, model
ORDER BY model_count DESC;

--STEP_4)Electric Range and Fuel Type Analysis
--Average Electric Range by Model

SELECT model, AVG(electric_range) AS avg_range
FROM electric_vehicle_data
GROUP BY model
ORDER BY avg_range DESC;

--Distribution by Clean Alternative Fuel Types

SELECT Clean_Alternative_Fuel_Vehicle_CAFV_Eligibility, COUNT(DOL_Vehicle_ID) AS fuel_type_count
FROM electric_vehicle_data
GROUP BY Clean_Alternative_Fuel_Vehicle_CAFV_Eligibility
ORDER BY fuel_type_count DESC;

--STEP_5)Base MSRP Analysis
--Average MSRP by Manufacturer

SELECT Make, AVG(base_msrp) AS avg_msrp
FROM electric_vehicle_data
GROUP BY Make
ORDER BY avg_msrp DESC;

--MSRP Distribution by County

SELECT county, AVG(base_msrp) AS avg_msrp
FROM electric_vehicle_data
GROUP BY county
ORDER BY avg_msrp DESC;

--STEP_6)Trends by Model Year
--Count of Vehicles by Model Year

SELECT model_year, COUNT(DOL_Vehicle_ID) AS yearly_count
FROM electric_vehicle_data
GROUP BY model_year
ORDER BY model_year;

--Average Electric Range Over Time

SELECT model_year, AVG(electric_range) AS
