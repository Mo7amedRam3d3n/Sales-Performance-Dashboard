Retail Sales Analysis (2023–2024) — Excel Power Query & Power Pivot
Project Overview
This project analyzes retail sales data across multiple branches, brands, and product categories for the years 2023 and 2024. Using Power Query for data cleaning/transformation and Power Pivot (DAX) for modeling, a Star Schema data model was built, along with a set of Pivot Tables and an interactive Dashboard to explore sales performance by branch, brand, category, payment method, and time.
Dataset
The raw data was provided as multiple Excel sheets:
* Branch — Branch ID, Name, City, Manager
* Brands — Brand ID, Name, Country of Origin
* Customer — Customer ID, Name & Email (combined), City, Country
* PaymentMethod — Payment ID, Payment Method name
* Product — Product ID, Name, Category, Brand, Price
* Sales2023 — Sales transactions for 2023 (SaleID, CustomerID, ProductID, BranchID, Date, Quantity, TotalAmount, PaymentMethod)
* Sales2024 — Sales transactions for 2024 (same structure as Sales2023)
Tools Used
* Microsoft Excel
* Power Query (data cleaning & transformation)
* Power Pivot / Data Model (relationships, Star Schema)
* DAX (measures & calculated columns)
* PivotTables & PivotCharts (dashboard visuals)
Steps Taken
1. Data Import
* Loaded every sheet into Power Query using Load To ? Only Create Connection.
2. Data Cleaning & Transformation
* Merged Sales2023 and Sales2024 into a single query named Sales.
* Branch: removed an empty column (Column5).
* Brands: removed empty columns (Column4 to Column8).
* Customer: split the combined Name;Email column into separate columns; applied Fill Down on the Country column to fill blank cells.
* PaymentMethod: removed an empty column (Column5).
* Product: applied Fill Down on the Category column; replaced a text error in the Price column with 0; removed empty columns (Column4 to Column8).
* Sales: changed the Date column data type to Date (3 rows with text errors were removed); changed the Quantity column data type to Whole Number (2 rows with text errors were removed).
* Removed duplicate rows from all dimension tables (all tables except Sales).
* Added a conditional column in Sales named Invoice Category: High if TotalAmount > 1000, otherwise Low.
* Closed & Loaded all queries into the Data Model.
3. Data Modeling (Star Schema)
Built a Star Schema with Sales as the central fact table:
* Branch ? Sales (BranchID)
* PaymentMethod ? Sales (PaymentMethod)
* Customer ? Sales (CustomerID)
* Product ? Sales (ProductID)
* Brands ? Product (BrandName ? Brand)
Also created a Calendar table from the Diagram View (Design ? Date Table ? New) to cover all dates continuously, since the Date column in Sales had missing days, and linked it to the Date column in Sales.
4. DAX Measures
* Total Sales = SUM(Sales[TotalAmount])
* Active Customers = DISTINCTCOUNT(Sales[CustomerID])
5. PivotTables
Several PivotTables were built from the Sales fact table to summarize Total Sales across different dimensions:
* Sales by Brand — Total Sales broken down for each of the 5 brands (Brand A–E).
* Sales by Category — Total Sales broken down for each product category (Fashion, Electronics, Beauty, Home, Sports).
* Sales by Branch — Total Sales broken down for each of the 5 branches.
* Sales by Payment Method — Total Sales broken down by payment type (PayPal, Credit Card, Cash, Bank Transfer).
* Sales by Month — Total Sales broken down across all 12 months, to observe seasonal trends.
* Category × Brand Matrix — A cross-tabulated PivotTable showing Total Sales for every combination of Category and Brand (rows = Category, columns = Brand), useful for identifying which brand performs best within each category.
In addition to these breakdowns, two overall summary metrics were calculated:
* Total Sales (Grand Total across all transactions)
* Active Customers (distinct count of customers who made at least one purchase)
6. Dashboard
Built an interactive dashboard combining PivotCharts:
* Sales per Branch
* Sales per Month
* Sales per Category
* Sales by Category & Brand
* Sales per Payment Method
* Sales per Brand
* Slicers for BrandName and Month to filter all visuals interactively
Key Insights
* Total Sales: 974,693 | Active Customers: 638
* Top Branch: Branch 3 (205,153) — Lowest: Branch 5 (182,583); performance across branches is fairly balanced.
* Top Category: Fashion (221,302), followed by Electronics (200,355); Sports was the lowest (180,259).
* Top Brand: Brand D (219,828); Lowest: Brand A (164,292).
* Top Payment Method: PayPal (268,474), followed by Credit Card (248,973); Bank Transfer was the least used (224,208).
* Peak Sales Month: August (94,159); sales dipped notably in February (83,658) and were lowest in November (74,303), suggesting a seasonal pattern worth further investigation.
* The Category × Brand matrix shows Brand D leads in Fashion and Home, while Brand C leads in Electronics — useful for brand-category strategy decisions.
How to Use
1. Download/clone the repository.
2. Open the Excel file and go to Data ? Queries & Connections to review the Power Query transformation steps.
3. Open the Data Model (Power Pivot) tab to explore the Star Schema relationships and DAX measures.
4. Go to the Dashboard sheet and use the BrandName and Month slicers to filter the visuals interactively.
5. PivotTables can be found on their dedicated sheets for a detailed breakdown of each dimension.
Author
Built by [Mohamed Ramadan] as a data analysis portfolio project.

