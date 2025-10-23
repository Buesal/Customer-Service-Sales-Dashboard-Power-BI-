# 🧡 DAX Measures — Customer Service & Sales Dashboard

---

## 1) Core KPIs

```DAX
Total Sales = 
    SUM ( 'Sales'[Sales Value] )

Total Orders =
    SUM ( 'Sales'[Orders] )

Average CSAT =
    AVERAGE ( 'Feedback'[CSAT] )

---  

## 2) Time Intelligence
-- Last Month (LM)

Sales LM =
    CALCULATE ( [Total Sales], DATEADD ( 'Calendar'[Date], -1, MONTH ) )

Orders LM =
    CALCULATE ( [Total Orders], DATEADD ( 'Calendar'[Date], -1, MONTH ) )

CSAT LM =
    CALCULATE ( [Average CSAT], DATEADD ( 'Calendar'[Date], -1, MONTH ) )

-- Last Year (LY) если нужно
Sales LY =
    CALCULATE ( [Total Sales], DATEADD ( 'Calendar'[Date], -1, YEAR ) )

---


## 3) Comparisons (% change)

Sales % LM =
VAR curr = [Total Sales]
VAR lm   = [Sales LM]
RETURN DIVIDE ( curr - lm, lm, 0 )

Orders % LM =
VAR curr = [Total Orders]
VAR lm   = [Orders LM]
RETURN DIVIDE ( curr - lm, lm, 0 )

CSAT Δ vs LM =
VAR curr = [Average CSAT]
VAR lm   = [CSAT LM]
RETURN curr - lm

---

## 4) Channel Metrics

Sales by Channel =
    SUMX ( VALUES ( 'Channel'[Channel] ), [Total Sales] )

Orders by Channel =
    SUMX ( VALUES ( 'Channel'[Channel] ), [Total Orders] )

CSAT by Channel =
    AVERAGEX ( VALUES ( 'Channel'[Channel] ), [Average CSAT] )

---

## 5) Category Metrics

Sales by Category =
    SUMX ( VALUES ( 'Category'[Category] ), [Total Sales] )

Orders by Category =
    SUMX ( VALUES ( 'Category'[Category] ), [Total Orders] )

CSAT by Category =
    AVERAGEX ( VALUES ( 'Category'[Category] ), [Average CSAT] )

---

## 6) Product Metrics

Sales by Product =
    SUMX ( VALUES ( 'Product'[Product] ), [Total Sales] )

Orders by Product =
    SUMX ( VALUES ( 'Product'[Product] ), [Total Orders] )

CSAT by Product =
    AVERAGEX ( VALUES ( 'Product'[Product] ), [Average CSAT] )

---

## 7) People Metrics (Agents / Managers / Shifts)

Sales by Agent =
    SUMX ( VALUES ( 'Agent'[agent_name] ), [Total Sales] )

Orders by Agent =
    SUMX ( VALUES ( 'Agent'[agent_name] ), [Total Orders] )

Sales by Manager =
    SUMX ( VALUES ( 'Manager'[manager_name] ), [Total Sales] )

CSAT by Shift =
    AVERAGEX ( VALUES ( 'Shift'[Shift] ), [Average CSAT] )

---

## 8) Helper Measures

Sales Contribution % =
VAR totalAll = CALCULATE ( [Total Sales], ALL ( 'Category' ) )
RETURN DIVIDE ( [Total Sales], totalAll, 0 )

Orders Contribution % =
VAR totalAll = CALCULATE ( [Total Orders], ALL ( 'Channel' ) )
RETURN DIVIDE ( [Total Orders], totalAll, 0 )

