
# Sales Report 

## Problem Statement
This Report analyzes the sales data of ABC company for fiscal year 2023 showcasing the performance of different products across categories. The report comprises of data from different countries helping the company to study its performance globally and make business decisions accordingly. It gives a comprehensive view of the revenue and profit generation of the company across numerous countries it operates in.


### Steps followed 
# Preparing Data 
- Step 1 : Load data into Power BI Desktop, dataset contains three excel files and one python script source table.
  
  Python script= Python.Execute("import pandas as pd#(lf)from io import StringIO#(lf)#(lf)data = """"""Exchange ID;ExchangeRate;Exchange Currency#(lf)1;1;USD#(lf)2;0,75;GBP#(lf)3;0,85;EUR#(lf)4;3,67;AED#(lf)5;1,3;AUD""""""#(lf)df = pd.read_csv(StringIO(data), sep=';')#(lf)#(lf)# Return the transformed dataframe#(lf)df")
  
- Step 2 : Merged Sales Table and Purchase Table and added Purchase Date column to the sales table. (Left Outer Join)
- Step 3 : Filtered the null values from Purchase Date column (Sales Table)
- Step 4 : Loaded the table into Power BI Desktop.
  
# Modelling 
- Step 5 :  Created two calculated tables
           1) Calender Table (Date Table):
  CALENDERAUTO()
  Month = MONTH(Calender[Date])
  Month Name = FORMAT(Calender[Date],"mmmm")
  Year = YEAR(Calender[Date])
  Quarter = "Q" & QUARTER(Calender[Date])
           2) Sales USD Table:
   Sales USD = ADDCOLUMNS(Sales,"Country Name",RELATED(Countries[Country]),"Exchange Rate", RELATED('df'[ExchangeRate]),
    "Exchange Currency", RELATED(df[Exchange Currency]),
    "Gross Revenue USD", [Gross Revenue] * RELATED(df[ExchangeRate]),
    "Net Revenue USD", [net revenue] * RELATED(df[ExchangeRate]),
    "Total Tax USD", [Total Tax] * RELATED(df[ExchangeRate]))"
             The Sales USD table converts the gross and net revenue data in the sales table           into US dollars by using the exchange rates provided in the "df" table.
- Step 6 : Modelled the data- created relationship between tables
  ![image](https://github.com/AmanBaker06/ChargedSyntax/assets/168013894/36b608a3-59fe-4def-a886-288cb9609f37)
- Step 7 : The following measures have been created in the Sales USD table
  Median= MEDIAN('Sales USD'[Gross Revenue USD])
  Quarterly Net Revenue Margin = SUMX('Sales USD','Sales USD'[Net Revenue USD]/'Sales USD'[Gross Revenue USD])
Quarterly Profit = CALCULATE(SUMX('Sales USD','Sales USD'[Gross Revenue USD]),DATESQTD(Calender[Date].[Date]))

# Report
Sales View

![image](https://github.com/AmanBaker06/ChargedSyntax/assets/168013894/9d5e11ae-b88f-4261-b755-44d5543c0bb9)


IMP: The line Chart shows Median Sales over time. It is also forecasting the sales for the next quarter with 99% confidence interval.

Profit View

  ![image](https://github.com/AmanBaker06/ChargedSyntax/assets/168013894/53effc9f-4979-4719-972c-4632508ee355)


The page focuses on the profit made by the products over time in the respective courses.

Sales_Rep Performance 

![image](https://github.com/AmanBaker06/ChargedSyntax/assets/168013894/fffe9e0d-f46f-4a9d-91d8-b5645365feab)


Performance Review of Sales Representatives in each country assessing which products they sold the most and how much revenue they generated for the company
 


