# Problem Statement
AtliQ Motors is an automotive giant from the USA specializing in electric vehicles (EV). In the last 5 years, their market share rose to 25% in electric and hybrid vehicles segment in North America. As a part of their expansion plans, they wanted to launch their bestselling models in India where their market share is less than 2%. Bruce Haryali, the chief of AtliQ Motors India wanted to do a detailed market study of existing EV/Hybrid market in India before proceeding further. Bruce gave this task to the data analytics team of AtliQ motors and Peter Pandey is the data analyst working in this team.

## 1. ASK
Chief: Bruce Haryali

### Questions: Preliminary Analysis
- List the top 3 and bottom 3 makers for the fiscal years 2023 and 2024 in terms of the number of 2-wheelers sold.
- Identify the top 5 states with the highest penetration rate in 2-wheeler and 4-wheeler EV sales in FY 2024.
- List the states with negative penetration (decline) in EV sales from 2022 to 2024?
- What are the quarterly trends based on sales volume for the top 5 EV makers (4-wheelers) from 2022 to 2024?
- How do the EV sales and penetration rates in Delhi compare to Karnataka for 2024?
- List down the compounded annual growth rate (CAGR) in 4-wheeler units for the top 5 makers from 2022 to 2024.
- List down the top 10 states that had the highest compounded annual growth rate (CAGR) from 2022 to 2024 in total vehicles sold.
- What are the peak and low season months for EV sales based on the data from 2022 to 2024?
- What is the projected number of EV sales (including 2-wheelers and 4-wheelers) for the top 10 states by penetration rate in 2030, based on the compounded annual growth rate (CAGR) from previous years
- Estimate the revenue growth rate of 4-wheeler and 2-wheelers EVs in India for 2022 vs 2024 and 2023 vs 2024, assuming an average unit price. Average Price =85K for 2-Wheeler, 15L for 4-Wheeler

### Questions: Secondary Analysis
- What are the primary reasons for customers choosing 4-wheeler EVs in 2023 and 2024 (cost savings, environmental concerns, government incentives)?
- How do government incentives and subsidies impact the adoption rates of 2-wheelers and 4-wheelers? Which states in India provided most subsidies?
- How does the availability of charging stations infrastructure correlate with the EV sales and penetration rates in the top 5 states?
- Who should be the brand ambassador if AtliQ Motors launches their EV/Hybrid vehicles in India and why?
- Which state of India is ideal to start the manufacturing unit? (Based on subsidies provided, ease of doing business, stability in governance etc.)
- Your top 3 recommendations for AtliQ Motors.


## 2. PREPARE
### Data Storage:
The public dataset is completely available on the Code basis website platform where it stores and consolidates all available datasets for analysis. The specific individual datasets at hand can be obtained at this link below: https://codebasics.io/challenge/codebasics-resume-project-challenge

### Data Organized:
The dataset is taken from the Vahan Sewa. Thanks to the Vahan Sewa for providing datasets for public access which is a great learning asset - feel free to explore them here: [Vahan Sewa](https://vahan.parivahan.gov.in/vahan4dashboard/vahan/view/reportview.xhtml) This dataset contains only 3 csv file and 1 text file (meta_data)

## 3. PROCESS
### Tools Used:
- Microsoft Excel
- Tableau

### Data Used:
dim_date, electric_vehicle_sales_by_makers, electric_vehicle_sales_by_state

### About Data:
Column Description for electric_vehicle_sales_by_state.csv:
- date: The date on which the data was recorded. Format: DD-MMM-YY. (Data is recorded on a monthly basis)
- state: The name of the state where the sales data is recorded. This indicates the geographical location within India.
- vehicle_category: The category of the vehicle, specifying whether it is a 2-Wheeler or a 4-Wheeler.
- electric_vehicles_sold: The number of electric vehicles sold in the specified state and category on the given date.
- total_vehicles_sold: The total number of vehicles (including both electric and non-electric) sold in the specified state and category on the given date.


Column Description for electric_vehicle_sales_by_makers.csv:
- date: The date on which the sales data was recorded. Format: DD-MMM-YY. (Data is recorded on a monthly basis)
- vehicle_category: The category of the vehicle, specifying whether it is a 2-Wheeler or a 4-Wheeler.
- maker: The name of the manufacturer or brand of the electric vehicle.
- electric_vehicles_sold: The number of electric vehicles sold by the specified maker in the given category on the given date.


Column Description for dim_date.csv:
- date: The specific date for which the data is relevant. Format: DD-MMM-YY. (Data is recorded on a monthly basis)
- fiscal_year: The fiscal year to which the date belongs. This is useful for financial and business analysis.
- quarter: The fiscal quarter to which the date belongs. Fiscal quarters are typically divided as Q1, Q2, Q3, and Q4.

### Data Cleaning & Transformation:
- Microsoft Excel, Power Query was used to clean and transform raw data.
- Duplicates were checked and removed.
- Gaps were checked with the TRIM function.
- DND -> Dadra Nagar and Haveli & Daman Diu, Andaman & Nicobar -> Andaman & Nicobar Islands
- Capitalized the maker columns

# 4. ANALYZE
Data Analyzing  
Tableau was used to analyze data.

### Key Metrics:
1. Fiscal Year: The fiscal year is a one-year period used for financial reporting and budgeting, starting on April 1st and ending on March 31st of the following year in India.
2. Penetration Rate: This metric represents the percentage of total vehicles that are electric within a specific region or category. It is calculated as:
		Penetration Rate =  (Electric Vehicles Sold / Total Vehicles Sold) * 100  
   This indicates the adoption level of electric vehicles.
3. Compound Annual Growth Rate (CAGR): CAGR measures the mean annual growth rate over a specified period longer than one year. It is calculated as:
		CAGR = [(Ending Value / Beginning Value) ** 1/n] -1

### Calculated Fields/ Parameters:
- Fiscal Year (Dis) = [Fiscal Year (Con)]
- FY Date? +9Mons = DATE(DATEADD('month',9,[Date]))
- Average Price? 85K|15L = IF [Vehicle Category]=="2-Wheelers" THEN 85000 ELSE 1500000 END
- Revenue? = [Average Price? 85K|15L]*[Electric Vehicles Sold]
- #of EV Sales @2030 = ROUND(IF [Vehicle Category - States]=="2-Wheelers" THEN POWER(1+0.9217,6)* [Electric Vehicles Sold - States] ELSE POWER(1+1.1628,6)* [Electric Vehicles Sold - States] END)
- %Difference Revenue = (SUM([CY Revenue])-SUM([PY Revenue])) / SUM([PY Revenue])
- %Difference Sales = (SUM([CY Sales])-SUM([PY Sales])) / SUM([PY Sales])
- %Difference Sales: EV = (SUM([CY Sales: EV])-SUM([PY Sales: EV])) / SUM([PY Sales: EV])
- Bottom N? T|F = INDEX()>[Bottom N]
- CAGR? EV Sold = POWER(ZN(SUM([Electric Vehicles Sold]))/LOOKUP(ZN(SUM([Electric Vehicles Sold])),-[N Years]), ZN(1/[N Years])) - 1
- CAGR? Total Vehicle Sold = POWER(ZN(SUM([Total Vehicles Sold]))/LOOKUP(ZN(SUM([Total Vehicles Sold])),-[N Years]),  ZN(1/[N Years])) - 1
- CY Revenue = IF [Fiscal Year (Dis)]=[Select Year] THEN [Revenue?] END
- CY Sales = IF [Fiscal Year (Dis)]=[Select Year] THEN [Total Vehicles Sold] END
- CY Sales: EV = IF [Fiscal Year (Dis)]=[Select Year] THEN [Electric Vehicles Sold] END
- Growth Rate 22 Vs 24 = ZN((SUM([Revenue?])-LOOKUP(SUM([Revenue?]),-2)) / LOOKUP(SUM([Revenue?]),-2))
- Growth Rate 23 Vs 24 = ZN((SUM([Revenue?])-LOOKUP(SUM([Revenue?]),-1)) /LOOKUP(SUM([Revenue?]),-1))
- Non EV Sales? = SUM([Total Vehicles Sold])-SUM([Electric Vehicles Sold - States])
- Penetration Rate? Dec = SUM([Electric Vehicles Sold - States])/SUM([Total Vehicles Sold])
- PY Revenue = IF [Fiscal Year (Dis)]=[Select Year]-1 THEN [Revenue?] END
- PY Sales = IF [Fiscal Year (Dis)]=[Select Year]-1 THEN [Total Vehicles Sold] END
- PY Sales: EV = IF [Fiscal Year (Dis)]=[Select Year]-1 THEN [Electric Vehicles Sold] END
- Top N? T|F = INDEX()<=[Top N]

# 5. SHARE

# 6. ACT	
### Insights:


### Recommendations:
Thank you for reading and evaluating my repo :)
Live Dashboard Link








