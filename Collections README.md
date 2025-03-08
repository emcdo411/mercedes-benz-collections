# Mercedes-Benz Collections Operations Database

## Overview
This repository contains SQL scripts and queries for analyzing **Mercedes-Benz Collections Operations**. The dataset simulates financial collections, delinquency reports, and payment recoveries, supporting **data-driven decision-making** in collections management.

## Database Setup
### Microsoft SQL Server (MSSQL)
#### Step 1: Create the Database
```sql
CREATE DATABASE MercedesBenzCollectionsDB;
GO
USE MercedesBenzCollectionsDB;
GO
```
#### Step 2: Create Tables
```sql
CREATE TABLE CollectionsData (
    AccountID INT PRIMARY KEY,
    CustomerName VARCHAR(100),
    AgentID INT,
    AgentName VARCHAR(100),
    PaymentDueDate DATE,
    DaysPastDue INT,
    OutstandingBalance DECIMAL(10,2),
    RecoveredAmount DECIMAL(10,2),
    PaymentStatus VARCHAR(20) CHECK (PaymentStatus IN ('On Time', 'Late', 'Default', 'Recovered'))
);
```
#### Step 3: Insert Sample Data
```sql
INSERT INTO CollectionsData (AccountID, CustomerName, AgentID, AgentName, PaymentDueDate, DaysPastDue, OutstandingBalance, RecoveredAmount, PaymentStatus)
VALUES
    (1001, 'John Doe', 201, 'Sarah Carter', '2024-01-15', 45, 1500.00, 0.00, 'Default'),
    (1002, 'Alice Smith', 202, 'Mike Johnson', '2024-02-10', 10, 700.00, 500.00, 'Late');
```

## Advanced SQL Queries
### 1. **Delinquent Account Report** (Accounts past due over 30 days)
```sql
SELECT AccountID, CustomerName, DaysPastDue, OutstandingBalance 
FROM CollectionsData
WHERE DaysPastDue > 30
ORDER BY DaysPastDue DESC;
```
### 2. **Recovery Performance Report** (Recovery percentage per agent)
```sql
SELECT AgentName, 
       COUNT(AccountID) AS TotalCases, 
       SUM(RecoveredAmount) / NULLIF(SUM(OutstandingBalance), 0) * 100 AS RecoveryRate 
FROM CollectionsData
GROUP BY AgentName
ORDER BY RecoveryRate DESC;
```

## Conclusion
This project provides structured **collections operations reporting** for **Mercedes-Benz Financial Services**, aiding in risk analysis, recovery tracking, and delinquency management.

🚀 **Use this for SQL learning, business analytics, and financial reporting automation!**

