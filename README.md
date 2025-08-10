# 📊 RFM Segmentation

## 🧠 What is RFM Segmentation?

**RFM Segmentation** is a powerful analytical technique used to evaluate and group customers based on their transaction history. It stands for:

* **Recency** – How recently a customer made a purchase.
* **Frequency** – How often they’ve purchased.
* **Monetary** – How much they’ve spent.

By analyzing these three metrics, businesses can categorize customers and design personalized strategies to improve engagement, retention, and profitability.

## 🎯 Why Perform RFM Segmentation?

Segmenting customers using RFM helps identify valuable customer types such as:

* Champions
* Loyal Customers
* Potential Loyalists
* Promising Customers
* Needs Attention
* At Risk
* Others

This process empowers businesses to focus marketing efforts, improve customer relationships, and maximize return on investment by treating each group based on its behavior.



## 🏗️ Database Setup
* Created a database named `RFM_SALES_DB`.

```sql
CREATE DATABASE IF NOT EXISTS RFM_SALES_DB;
USE RFM_SALES_DB;
CREATE TABLE SALES_DATA (
  ORDERNUMBER INT,
  QUANTITYORDERED DECIMAL(10,2),
  PRICEEACH DECIMAL(10,2),
  ORDERLINENUMBER INT,
  SALES DECIMAL(10,2),
  ORDERDATE VARCHAR(20),
  STATUS VARCHAR(20),
  QTR_ID INT,
  MONTH_ID INT,
  YEAR_ID INT,
  PRODUCTLINE VARCHAR(40),
  MSRP INT,
  PRODUCTCODE VARCHAR(20),
  CUSTOMERNAME VARCHAR(70),
  PHONE VARCHAR(30),
  ADDRESSLINE1 VARCHAR(80),
  ADDRESSLINE2 VARCHAR(80),
  CITY VARCHAR(30),
  STATE VARCHAR(30),
  POSTALCODE VARCHAR(20),
  COUNTRY VARCHAR(30),
  TERRITORY VARCHAR(30),
  CONTACTLASTNAME VARCHAR(30),
  CONTACTFIRSTNAME VARCHAR(30),
  DEALSIZE VARCHAR(15)
);

```

* 📁 Data was imported locally into the `SALES_DATA` table.


## Dataset Exploration

### Preview Records
```sql
SELECT * FROM SALES_DATA LIMIT 5;
```

-- OUTPUT --

| ORDERNUMBER | QUANTITYORDERED | PRICEEACH | ORDERLINENUMBER | SALES   | ORDERDATE | STATUS  | QTR_ID | MONTH_ID | YEAR_ID | PRODUCTLINE  | MSRP | PRODUCTCODE | CUSTOMERNAME              | PHONE         | ADDRESSLINE1               | ADDRESSLINE2 | CITY          | STATE | POSTALCODE | COUNTRY | TERRITORY | CONTACTLASTNAME | CONTACTFIRSTNAME | DEALSIZE |
|-------------|------------------|-----------|------------------|---------|------------|---------|--------|-----------|---------|--------------|------|--------------|----------------------------|---------------|-----------------------------|---------------|---------------|--------|-------------|---------|-----------|------------------|-------------------|----------|
| 10107       | 30.00            | 95.70     | 2                | 2871.00 | 24/2/03    | Shipped | 1      | 2         | 2003    | Motorcycles  | 95   | S10_1678     | Land of Toys Inc.         | 2125557818    | 897 Long Airport Avenue    |               | NYC           | NY     | 10022       | USA     | NA        | Yu               | Kwai              | Small    |
| 10121       | 34.00            | 81.35     | 5                | 2765.90 | 7/5/03     | Shipped | 2      | 5         | 2003    | Motorcycles  | 95   | S10_1678     | Reims Collectables         | 26.47.1555    | 59 rue de l'Abbaye          |               | Reims         |        | 51100       | France  | EMEA      | Henriot          | Paul              | Small    |
| 10134       | 41.00            | 94.74     | 2                | 3884.34 | 1/7/03     | Shipped | 3      | 7         | 2003    | Motorcycles  | 95   | S10_1678     | Lyon Souveniers            | +33 1 46 62 7555 | 27 rue du Colonel Pierre Avia |            | Paris         |        | 75508       | France  | EMEA      | Da Cunha         | Daniel            | Medium   |
| 10145       | 45.00            | 83.26     | 6                | 3746.70 | 25/8/03    | Shipped | 3      | 8         | 2003    | Motorcycles  | 95   | S10_1678     | Toys4GrownUps.com          | 6265557265    | 78934 Hillside Dr.         |               | Pasadena      | CA     | 90003       | USA     | NA        | Young            | Julie             | Medium   |
| 10159       | 49.00            | 100.00    | 14               | 5205.27 | 10/10/03   | Shipped | 4      | 10        | 2003    | Motorcycles  | 95   | S10_1678     | Corporate Gift Ideas Co.   | 6505551386    | 7734 Strong St.            |               | San Francisco | CA     |             | USA     | NA        | Brown            | Julie             | Medium   |


```sql
SELECT COUNT(*) As ROW_COUNT FROM SALES_DATA;
```

-- OUTPUT --

| ROW_COUNT |
|-----------|
| 2823      |


# Checking unique values
```sql
SELECT DISTINCT YEAR_ID FROM SALES_DATA;
```

-- OUTPUT --

| YEAR_ID |
|---------|
| 2003    |
| 2004    |
| 2005    |


```sql
SELECT DISTINCT STATUS FROM SALES_DATA;
```

-- OUTPUT --

| STATUS     |
|------------|
| Shipped    |
| Disputed   |
| In Process |
| Cancelled  |
| On Hold    |
| Resolved   |


```sql
SELECT DISTINCT PRODUCTLINE FROM SALES_DATA;
```

-- OUTPUT --

| PRODUCTLINE       |
|-------------------|
| Motorcycles       |
| Classic Cars      |
| Trucks and Buses  |
| Vintage Cars      |
| Planes            |
| Ships             |
| Trains            |


```sql
SELECT DISTINCT COUNTRY FROM SALES_DATA;
```

-- OUTPUT --


| COUNTRY      |
|--------------|
| USA          |
| France       |
| Norway       |
| Australia    |
| Finland      |
| Austria      |
| UK           |
| Spain        |
| Sweden       |
| Singapore    |
| Canada       |
| Japan        |
| Italy        |
| Denmark      |
| Belgium      |
| Philippines  |
| Germany      |
| Switzerland  |
| Ireland      |



```sql
SELECT DISTINCT DEALSIZE FROM SALES_DATA;
```

-- OUTPUT --

| DEALSIZE |
|----------|
| Small    |
| Medium   |
| Large    |


```sql
SELECT DISTINCT TERRITORY FROM SALES_DATA;
```

-- OUTPUT --

| TERRITORY |
|-----------|
| NA        |
| EMEA      |
| APAC      |
| Japan     |


```sql
SELECT DISTINCT CITY FROM SALES_DATA;
```

-- OUTPUT --

| CITY          |
|---------------|
| NYC           |
| Reims         |
| Paris         |
| Pasadena      |
| San Francisco |
| Burlingame    |
| Lille         |
| Bergen        |
| Melbourne     |
| Newark        |
| Bridgewater   |
| Nantes        |
| Cambridge     |
| Helsinki      |
| Stavern       |
| Allentown     |
| Salzburg      |
| Chatswood     |
| New Bedford   |
| Liverpool     |
| Madrid        |
| Lule          |
| Singapore     |
| South Brisbane|
| Philadelphia  |
| Lyon          |
| Vancouver     |
| Burbank       |
| New Haven     |
| Minato-ku     |
| Torino        |
| Boras         |
| Versailles    |
| San Rafael    |
| Nashua        |
| Brickhaven    |
| North Sydney  |
| Montreal      |
| Osaka         |
| White Plains  |
| Kobenhavn     |
| London        |
| Toulouse      |
| Barcelona     |
| Los Angeles   |
| San Diego     |
| Bruxelles     |
| Tsawassen     |
| Boston        |
| Cowes         |
| Oulu          |
| San Jose      |
| Graz          |
| Makati City   |
| Marseille     |
| Koln          |
| Gensve        |
| Reggio Emilia |
| Frankfurt     |
| Espoo         |
| Dublin        |
| Manchester    |
| Aaarhus       |
| Glendale      |
| Sevilla       |
| Brisbane      |
| Strasbourg    |
| Las Vegas     |
| Oslo          |
| Bergamo       |
| Glen Waverly  |
| Munich        |
| Charleroi     |


```sql
SELECT DISTINCT STATE FROM SALES_DATA;
```

-- OUTPUT --

| STATE         |
|---------------|
| NY            |
|               |
| CA            |
| Victoria      |
| NJ            |
| CT            |
| MA            |
| PA            |
| NSW           |
| Queensland    |
| BC            |
| Tokyo         |
| NH            |
| Quebec        |
| Osaka         |
| Isle of Wight |
| NV            |


# Analysis 

## RFM Segmentation

### RFM Metric Calculation
* **This query calculates the RFM metrics (Recency, Frequency, Monetary) for each customer.**

```sql
 SELECT 
    CUSTOMERNAME,
    DATEDIFF(
      (SELECT MAX(STR_TO_DATE(ORDERDATE, '%d/%m/%y')) FROM SALES_DATA),
      MAX(STR_TO_DATE(ORDERDATE, '%d/%m/%y'))) AS RECENCY_VALUE,
    COUNT(DISTINCT ORDERNUMBER) AS FREQUENCY_VALUE,
    ROUND(SUM(SALES), 0) AS MONETARY_VALUE
  FROM SALES_DATA
  GROUP BY CUSTOMERNAME;
  ```

-- OUTPUT --

| CUSTOMERNAME                   | RECENCY_VALUE | FREQUENCY_VALUE | MONETARY_VALUE |
|--------------------------------|---------------|------------------|-----------------|
| Alpha Cognac                   | 64            | 3                | 70488           |
| Amica Models & Co.             | 264           | 2                | 94117           |
| Anna's Decorations, Ltd        | 83            | 4                | 153996          |
| Atelier graphique              | 187           | 3                | 24180           |
| Australian Collectables, Ltd   | 22            | 3                | 64591           |
| ...                            | ...           | ...              | ...             |

* **This query creates a view named RFM_SEGMENTATION_VIEW that calculates Recency, Frequency, and Monetary scores for each customer, combines them into RFM scores, and classifies customers into business-relevant segments like Champions, Loyal, or At Risk.**

```sql
CREATE OR REPLACE VIEW RFM_SEGMENTATION_VIEW AS
WITH CUSTOMER_SUMMARY_TABLE AS (
  SELECT 
    CUSTOMERNAME,
    DATEDIFF(
      (SELECT MAX(STR_TO_DATE(ORDERDATE, '%d/%m/%y')) FROM SALES_DATA),
      MAX(STR_TO_DATE(ORDERDATE, '%d/%m/%y'))
    ) AS RECENCY_VALUE,
    COUNT(DISTINCT ORDERNUMBER) AS FREQUENCY_VALUE,
    ROUND(SUM(SALES), 0) AS MONETARY_VALUE
  FROM SALES_DATA
  GROUP BY CUSTOMERNAME
),

RFM_SCORE AS (
  SELECT 
    *,
    NTILE(5) OVER (ORDER BY RECENCY_VALUE DESC) AS R_SCORE,
    NTILE(5) OVER (ORDER BY FREQUENCY_VALUE ASC) AS F_SCORE,
    NTILE(5) OVER (ORDER BY MONETARY_VALUE ASC) AS M_SCORE
  FROM CUSTOMER_SUMMARY_TABLE
),

RFM_COMBINATION_SCORE AS (
  SELECT 
    *,
    (R_SCORE + F_SCORE + M_SCORE) AS TOTAL_RFM_SCORE,
    CONCAT(R_SCORE, F_SCORE, M_SCORE) AS RFM_SCORE_COMBINATION
  FROM RFM_SCORE
)

SELECT 
  RC.*,
  CASE
    WHEN RFM_SCORE_COMBINATION IN ('555', '554', '545', '544', '554', '553', '543') THEN 'Champions'
    WHEN RFM_SCORE_COMBINATION IN ('445', '454', '355', '344', '443', '535', '453') THEN 'Loyal Customers'
    WHEN RFM_SCORE_COMBINATION IN ('344', '343', '342', '333', '434') THEN 'Potential Loyalists'
    WHEN RFM_SCORE_COMBINATION IN ('322', '323', '332', '233', '243', '242', '224') THEN 'Promising Customers'
    WHEN RFM_SCORE_COMBINATION IN ('213', '214', '223', '232', '221', '222') THEN 'Needs Attention'
    WHEN RFM_SCORE_COMBINATION IN ('111', '112', '113', '122', '121') THEN 'At Risk'
    ELSE 'Others'
  END AS CUSTOMER_SEGMENT
FROM RFM_COMBINATION_SCORE AS RC;

```
* **Show RFM Scores**
```sql
SELECT 
  CUSTOMERNAME, 
  TOTAL_RFM_SCORE, 
  RFM_SCORE_COMBINATION
FROM RFM_SEGMENTATION_VIEW;
```
 
-- OUTPUT --

| CUSTOMERNAME              | TOTAL_RFM_SCORE | RFM_SCORE_COMBINATION |
|---------------------------|------------------|------------------------|
| Boards & Toys Co.         | 7                | 421                    |
| Atelier graphique         | 7                | 331                    |
| Auto-Moto Classics Inc.   | 7                | 331                    |
| Microscale Inc.           | 4                | 211                    |
| Royale Belge              | 10               | 451                    |
| ...                       | ...              | ...                    |

* **This query shows RFM Comobination Scores**
```sql
SELECT DISTINCT RFM_SCORE_COMBINATION
FROM RFM_SEGMENTATION_VIEW
ORDER BY RFM_SCORE_COMBINATION;
```

-- OUTPUT --

| RFM_SCORE_COMBINATION |
|------------------------|
| 111                    |
| 112                    |
| 113                    |
| 114                    |
| 124                    |
| ...                    |


* **This query assigns each customer to an RFM-based segment (like Champions, Loyal Customers, At Risk, etc.) based on their combined RFM score pattern.**

```sql
SELECT 
  CUSTOMERNAME ,
  CASE
    WHEN RFM_SCORE_COMBINATION IN ('555', '554', '545', '544', '554', '553', '543') THEN 'Champions'
    WHEN RFM_SCORE_COMBINATION IN ('445', '454', '355', '344', '443', '535', '453') THEN 'Loyal Customers'
    WHEN RFM_SCORE_COMBINATION IN ('344', '343', '342', '333', '434') THEN 'Potential Loyalists'
    WHEN RFM_SCORE_COMBINATION IN ('322', '323', '332', '233', '243', '242', '224') THEN 'Promising Customers'
    WHEN RFM_SCORE_COMBINATION IN ('213', '214', '223', '232', '221', '222') THEN 'Needs Attention'
    WHEN RFM_SCORE_COMBINATION IN ('111', '112', '113', '122', '121') THEN 'At Risk'
    ELSE 'Others'
  END AS CUSTOMER_SEGMENT
FROM RFM_SEGMENTATION_VIEW;
```

-- OUTPUT --

| CUSTOMERNAME                 | CUSTOMER_SEGMENT      |
|------------------------------|------------------------|
| Signal Gift Stores           | Potential Loyalists    |
| Gifts4AllAges.com            | Champions              |
| Collectables For Less Inc.   | Others                 |
| Toms Spezialitten, Ltd       | Needs Attention        |
| FunGiftIdeas.com             | Loyal Customers        |
| Super Scale Inc.             | At Risk                |
| ...                          | ...                    |

* **This query groups customers by their RFM segment (like 'Champions', 'At Risk', etc.) and returns the number of customers in each segment, ordered from most to least.**

```sql
WITH CTE_EXAMPLE AS (
SELECT 
  CUSTOMERNAME ,
  CASE
    WHEN RFM_SCORE_COMBINATION IN ('555', '554', '545', '544', '554', '553', '543') THEN 'Champions'
    WHEN RFM_SCORE_COMBINATION IN ('445', '454', '355', '344', '443', '535', '453') THEN 'Loyal Customers'
    WHEN RFM_SCORE_COMBINATION IN ('344', '343', '342', '333', '434') THEN 'Potential Loyalists'
    WHEN RFM_SCORE_COMBINATION IN ('322', '323', '332', '233', '243', '242', '224') THEN 'Promising Customers'
    WHEN RFM_SCORE_COMBINATION IN ('213', '214', '223', '232', '221', '222') THEN 'Needs Attention'
    WHEN RFM_SCORE_COMBINATION IN ('111', '112', '113', '122', '121') THEN 'At Risk'
    ELSE 'Others'
  END AS CUSTOMER_SEGMENT
FROM RFM_SEGMENTATION_VIEW
)

SELECT CUSTOMER_SEGMENT, COUNT(*) AS NO_OF_CUSTOMERS
FROM CTE_EXAMPLE 
GROUP BY CUSTOMER_SEGMENT
ORDER BY NO_OF_CUSTOMERS DESC;
```

-- OUTPUT --

| CUSTOMER_SEGMENT       | NO_OF_CUSTOMERS |
|------------------------|------------------|
| Others                 | 32               |
| At Risk                | 16               |
| Champions              | 14               |
| Needs Attention        | 9                |
| Promising Customers    | 9                |
| Potential Loyalists    | 6                |
| Loyal Customers        | 6                |














