# Creditcard_Dashboard
Power BI Dashboard about credit card users
CREDIT CARD WEEKLY STATUS REPORT
Dashboard link:https://app.powerbi.com/links/fMyh6qlUCj?ctid=7e2137dd-6ef9-46eb-974e-5086fd7cdd20&pbi_source=linkShare
Project Objective
To create an all-inclusive weekly credit card dashboard that delivers real-time insights into crucial performance metrics and trends, allowing stakeholders to efficiently monitor and analyze credit card operations.

Import data to SQL database
1. Prepare csv file
2. Create tables in mySQL
3. import csv file into mySQL

DAX Queries
Age group
age_group = switch(
    true(),
    customer[Customer_Age]<30,"20-30",
    customer[Customer_Age]>=30 && customer[Customer_Age]<40,"30-40",
    customer[Customer_Age]>=40 && customer[Customer_Age]<50,"40-50",
    customer[Customer_Age]>=50 && customer[Customer_Age]<60,"50-60",
    customer[Customer_Age]>=60,"60+","unknown")
Income group
income_group = switch(
    true(),
    customer[Income]<35000, "Less than 35000",
    customer[Income]>=35000 && customer[Income]<70000,"35000-70000",
     customer[Income]>=70000, "Above 70000","unknown"
)

Revenue
Revenue = credit_card[Annual_Fees]+credit_card[Total_Trans_Amt]+credit_card[Interest_Earned]

Current week revenue

Week_num2
week_num2 = WEEKNUM(credit_card[Week_Start_Date])


Week on week Revenue
week_Revenue = calculate( 
    sum(credit_card[Revenue]),
    filter(
        all(credit_card),credit_card[week_num2]=max(credit_card[week_num2])))
Previous week revenue
Previous_week_Revenue = calculate( 
    sum(credit_card[Revenue]),
    filter(
        all(credit_card),credit_card[week_num2]=max(credit_card[week_num2])-1))
Revenue change percentage
wow_revenue_change = divide(([week_Revenue]-[Previous_week_Revenue]),[Previous_week_Revenue])

Project Insight (Week 52)
Overview YTD:
• Overall revenue is 55M
• Total interest is 8M
• Total transaction amount is 45M
• Male customers are contributing more in revenue 30M, female 25M
