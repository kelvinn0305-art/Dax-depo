# 📊 Power BI Sales Analysis Project

## 📌 Project Overview

This Power BI project demonstrates advanced data analysis using:

* Calculated Columns
* DAX Measures
* Quick Measures
* Time Intelligence Functions
* Matrix-based Analysis
* Filter Context
* Relationships and RELATED()
* Iterator Functions

The dashboard helps analyze:

* Sales performance
* Profitability
* Return analysis
* Regional performance
* Time-based trends

---

# 📂 Dataset Information

## Fact Table

### `Sales_Fact`

Contains transactional sales records.

Columns:

* SalesID
* CustomerID
* ProductKey
* RegionID
* DateKey
* SalesAmount
* Cost
* Quantity
* ReturnID

---

## Dimension Tables

### `Customer_Dim`

Customer details table.

### `Region_Dim`

Region information table.

### `Date Table`

Used for Time Intelligence calculations.

---

# 🧮 Calculated Columns

## 1️⃣ Profit Column

```DAX
Profit = Sales_Fact[SalesAmount] - Sales_Fact[Cost]
```

Purpose:

* Calculates profit for each transaction.

---

## 2️⃣ Return Flag

```DAX
ReturnFlag =
IF(
    ISBLANK(Sales_Fact[ReturnID]),
    "Not Returned",
    "Returned"
)
```

Purpose:

* Identifies returned products.

---

## 3️⃣ Customer Full Name

```DAX
Customer Full Name =
Customer_Dim[First Name] & " " & Customer_Dim[Last Name]
```

Purpose:

* Combines first and last names.

---

# 📊 Measures

## Total Sales

```DAX
Total Sales =
SUM(Sales_Fact[SalesAmount])
```

---

## Total Cost

```DAX
Total Cost =
SUM(Sales_Fact[Cost])
```

---

## Total Profit

```DAX
Total Profit =
SUM(Sales_Fact[Profit])
```

---

## Return Rate %

```DAX
Return Rate % =
DIVIDE(
    COUNT(Sales_Fact[ReturnID]),
    COUNT(Sales_Fact[SalesID]),
    0
)
```

---

## Average Sale per Transaction

```DAX
Average Sale =
AVERAGE(Sales_Fact[SalesAmount])
```

---

# ⚡ Quick Measures

## Year-over-Year Growth

```DAX
YOY Growth =
[Total Sales] -
CALCULATE(
    [Total Sales],
    SAMEPERIODLASTYEAR('Date'[Date])
)
```

---

## Previous Month Difference

```DAX
Previous Month Difference =
[Total Sales] -
CALCULATE(
    [Total Sales],
    DATEADD('Date'[Date], -1, MONTH)
)
```

---

# 🗂️ Measure Management

Created a dedicated measure table to organize DAX measures clearly.

```DAX
Measure Table = { BLANK() }
```

---

# 🎛️ Filter Context & Behavior

## Using ALL()

```DAX
Sales Ignore Filters =
CALCULATE(
    [Total Sales],
    ALL(Sales_Fact)
)
```

Purpose:

* Removes filters during calculation.

---

# 🔧 DAX Functions Used

## Aggregation Functions

* SUM()
* AVERAGE()
* MAX()
* COUNT()
* DISTINCTCOUNT()

## Logical Functions

* IF()
* AND()
* OR()
* SWITCH()

## Text Functions

* CONCATENATE()
* UPPER()
* LEFT()

## Date Functions

* YEAR()
* MONTH()
* EOMONTH()

---

# 🔗 Joining & Relationships

## RELATED() Function

```DAX
Region Name =
RELATED(Region_Dim[RegionName])
```

Purpose:

* Pulls related data from dimension tables.

---

# 📅 Time Intelligence (Matrix-Based Analysis)

## TOTALYTD()

```DAX
Total YTD Sales =
TOTALYTD(
    [Total Sales],
    'Date'[Date]
)
```

---

## SAMEPERIODLASTYEAR()

```DAX
Sales LY =
CALCULATE(
    [Total Sales],
    SAMEPERIODLASTYEAR('Date'[Date])
)
```

---

## DATESINPERIOD()

```DAX
Last 3 Months Sales =
CALCULATE(
    [Total Sales],
    DATESINPERIOD(
        'Date'[Date],
        MAX('Date'[Date]),
        -3,
        MONTH
    )
)
```

---

## Running Total

```DAX
Running Total =
CALCULATE(
    [Total Sales],
    DATESBETWEEN(
        'Date'[Date],
        BLANK(),
        MAX('Date'[Date])
    )
)
```

---

# 🧠 Additional Scenarios

## SWITCH() Function

```DAX
Sales Category =
SWITCH(
    TRUE(),
    [Total Sales] < 1000, "Low",
    [Total Sales] < 5000, "Medium",
    "High"
)
```

---

## SUMX()

```DAX
Total Revenue =
SUMX(
    Sales_Fact,
    Sales_Fact[Quantity] * Sales_Fact[SalesAmount]
)
```

---

## AVERAGEX()

```DAX
Average Revenue =
AVERAGEX(
    Sales_Fact,
    Sales_Fact[Quantity] * Sales_Fact[SalesAmount]
)
```

---

# 📈 Matrix Visual Analysis

### Rows

* Year
* Month
* Region

### Values

* Total Sales
* Total Profit
* Running Total
* YTD Sales
* Return Rate %

---

# 📷 Dashboard Features

✅ KPI Cards
✅ Matrix Analysis
✅ Sales Trend Analysis
✅ Profit Tracking
✅ Return Analysis
✅ Regional Analysis
✅ Interactive Slicers
✅ Time Intelligence Reporting

---

# 🛠️ Tools & Technologies

* Power BI Desktop
* DAX
* Power Query
* Excel Dataset

---

# 📚 Key Learnings

* Understanding filter context
* Advanced DAX calculations
* Time intelligence analysis
* Relationship modeling
* Matrix visual reporting
* Iterator functions
* Measure management

---

# 🚀 Future Improvements

* Forecasting visuals
* Drill-through reports
* Mobile dashboard layout
* Row-Level Security (RLS)
* Power BI Service publishing



