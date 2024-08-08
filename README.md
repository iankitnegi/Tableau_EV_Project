# Problem Statement
AtliQ Motors is an automotive giant from the USA specializing in electric vehicles (EV). In the last 5 years, their market share rose to 25% in electric and hybrid vehicles segment in North America. As a part of their expansion plans, they wanted to launch their bestselling models in India where their market share is less than 2%. Bruce Haryali, the chief of AtliQ Motors India wanted to do a detailed market study of existing EV/Hybrid market in India before proceeding further. Bruce gave this task to the data analytics team of AtliQ motors and Peter Pandey is the data analyst working in this team.

## 1. ASK
Chief: Bruce Haryali

### Questions:  
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


## 2. PREPARE
### Data Storage:
The public dataset is completely available on the Code basis website platform where it stores and consolidates all available datasets for analysis. The specific individual datasets at hand can be obtained at this link below: https://codebasics.io/challenge/codebasics-resume-project-challenge

### Data Organized:
The dataset is taken from the Vahan Sewa. Thanks to the Vahan Sewa for providing datasets for public access which is a great learning asset - feel free to explore them here: [Vahan Sewa](https://vahan.parivahan.gov.in/vahan4dashboard/vahan/view/reportview.xhtml)  
This dataset contains only 3 csv file and 1 text file (meta_data)

## 3. PROCESS
### Tools Used:
- Microsoft Excel
- Tableau

### Data Used:
dim_customers, fact_spends

About Data:
Column Description for dim_customers:

customer_id: This column represents the Unique ID assigned to each customer.
gender: This column represents the gender of the customer. (Male, Female)
age_group: This column categorizes the customer into different age groups. (21-24, 25-34, 35-45, 45+)
marital_status: This column indicates the marital status of the customer (single, married).
city: This column represents the city of residence for the customer. (Mumbai, Delhi-NCR, Chennai, Hyderabad, Bengaluru)
occupation: This column denotes the occupation or profession of the customer. (Salaried IT Employees, Salaried Other Employees, Business Owners, Freelancers, Government Employees)
average_income: This column indicates the monthly average income of the customer, in INR currency.
Column Description for fact_spends:

customer_id: This column represents the Unique ID of each customer, linking to the dim_customer table.
month: This column indicates the month in which the spending was recorded. (May, June, July, August, September, October)
category: This column describes the category of spending (Entertainment, Apparel, Electronics, etc).
payment_type: This column specifies the type of payment used by the customer (Debit Card, Credit Card, UPI, Net Banking).
spends: This column shows the total amount spent by the customer in the specified month, category and payment_type.
Data Cleaning & Transformation:
Microsoft Excel was used to clean and transform raw data.
Duplicates were checked and removed.
Gaps were checked with the TRIM function.
Delhi NCR change into New Delhi
4. ANALYZE
Data Analyzing
Power BI was used to analyze data.

Key Metrics:
Avg income utilisation%: Find the average income utilisation % of customers (avg_spends/avg_income). The higher the average income utilisation%, the more is their likelihood to use credit cards.

KPIs:
Annual Expenditure = [Expenditure]*2
Annual Income = [Income]*2
Average Monthly Spend = AVERAGE(fact_spends[spend])
Credit Card = CALCULATE([Utilisation %], fact_spends[payment_type]="Credit Card")
Customers = COUNT(dim_customers[customer_id])
Expenditure = SUM(fact_spends[spend])
Expenditure* = SUM(fact_spends[spend])/6
Female = CALCULATE([Customers], dim_customers[gender]="Female")
Female Utilization = CALCULATE([Utilisation %], dim_customers[gender]="Female")
Income = SUM(dim_customers[income])
Income* = SUM(dim_customers[avg_income])
Male = CALCULATE([Customers], dim_customers[gender]="Male")
Male Utilization = CALCULATE([Utilisation %], dim_customers[gender]="Male")
Male% = [Male]/[Customers]
Net Banking = CALCULATE([Utilisation %], fact_spends[payment_type]="Net Banking")
Saving = [Income]-[Expenditure]
Saving* = [Income*]-[Expenditure*]
Transaction = COUNT(fact_spends[customer_id])
UPI = CALCULATE([Utilisation %], fact_spends[payment_type]="UPI")
Utilisation % = [Expenditure*]/[Income*]
5. SHARE
