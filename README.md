# RFM Segmentation
RFM (Recency, Frequency, Monetary) segmentation is a technique businesses use to classify customers according to their purchasing behavior. It provides insights into customer value and patterns, supporting more effective marketing and relationship management strategies

## Why follow this process
RFM segmentation calculates recency, frequency, and monetary scores for every customer and classifies them into segments according to these values. The included SQL script assigns customers into categories such as 'Churned Customer', 'Slipping Away, Cannot Lose', 'New Customers', 'Potential Churners', 'Active', and 'Loyal'.

## Database Preparation
- Create a database named `RFM_SALES`.
```sql
CREATE DATABASE IF NOT EXISTS RFM_SALES;
USE RFM_SALES;
CREATE TABLE SALES_SAMPLE_DATA (
    ORDERNUMBER INT(8),
    QUANTITYORDERED DECIMAL(8,2),
    PRICEEACH DECIMAL(8,2),
    ORDERLINENUMBER INT(3),
    SALES DECIMAL(8,2),
    ORDERDATE VARCHAR(16),
    STATUS VARCHAR(16),
    QTR_ID INT(1),
    MONTH_ID INT(2),
    YEAR_ID INT(4),
    PRODUCTLINE VARCHAR(32),
    MSRP INT(8),
    PRODUCTCODE VARCHAR(16),
    CUSTOMERNAME VARCHAR(64),
    PHONE VARCHAR(32),
    ADDRESSLINE1 VARCHAR(64),
    ADDRESSLINE2 VARCHAR(64),
    CITY VARCHAR(16),
    STATE VARCHAR(16),
    POSTALCODE VARCHAR(16),
    COUNTRY VARCHAR(24),
    TERRITORY VARCHAR(24),
    CONTACTLASTNAME VARCHAR(16),
    CONTACTFIRSTNAME VARCHAR(16),
    DEALSIZE VARCHAR(10)
);
```

- Import wizard data

## Dataset Exploration

```sql
SELECT * FROM SALES_SAMPLE_DATA LIMIT 5;
```
-- OUTPUT --

| ORDERNUMBER | QUANTITYORDERED | PRICEEACH | ORDERLINENUMBER | SALES   | ORDERDATE | STATUS  | QTR_ID | MONTH_ID | YEAR_ID | PRODUCTLINE | MSRP | PRODUCTCODE | CUSTOMERNAME          | PHONE       | ADDRESSLINE1            | ADDRESSLINE2 | CITY          | STATE | POSTALCODE | COUNTRY | TERRITORY | CONTACTLASTNAME | CONTACTFIRSTNAME | DEALSIZE |
|-------------|------------------|-----------|------------------|---------|-----------|---------|--------|----------|---------|-------------|------|-------------|-----------------------|-------------|-------------------------|--------------|---------------|-------|------------|---------|-----------|-----------------|------------------|----------|
| 10107       | 30.00            | 95.70     | 2                | 2871.00 | 24/2/03   | Shipped | 1      | 2        | 2003    | Motorcycles | 95   | S10_1678    | Land of Toys Inc.     | 2125557818  | 897 Long Airport Avenue |              | NYC           | NY    | 10022      | USA     | NA        | Yu              | Kwai             | Small    |
| 10121       | 34.00            | 81.35     | 5                | 2765.90 | 7/5/03    | Shipped | 2      | 5        | 2003    | Motorcycles | 95   | S10_1678    | Reims Collectables    | 26.47.1555  | 59 rue de l'Abbaye     |              | Reims         |       | 51100      | France  | EMEA       | Henriot         | Paul             | Small    |
| 10134       | 41.00            | 94.74     | 2                | 3884.34 | 1/7/03    | Shipped | 3      | 7        | 2003    | Motorcycles | 95   | S10_1678    | Lyon Souveniers       | +33 1 46 62 7555 | 27 rue du Colonel Pierre Avia |              | Paris         |       | 75508      | France  | EMEA       | Da Cunha        | Daniel           | Medium   |
| 10145       | 45.00            | 83.26     | 6                | 3746.70 | 25/8/03   | Shipped | 3      | 8        | 2003    | Motorcycles | 95   | S10_1678    | Toys4GrownUps.com     | 6265557265  | 78934 Hillside Dr.     |              | Pasadena      | CA    | 90003      | USA     | NA        | Young           | Julie            | Medium   |
| 10159       | 49.00            | 100.00    | 14               | 5205.27 | 10/10/03  | Shipped | 4      | 10       | 2003    | Motorcycles | 95   | S10_1678    | Corporate Gift Ideas Co. | 6505551386  | 7734 Strong St.        |              | San Francisco | CA    |            | USA     | NA        | Brown           | Julie            | Medium   |
