# SQL-LEARN
SELECT TOP (1000) [InvoiceNo]
      ,[StockCode]
      ,[Description]
      ,[Quantity]
      ,[InvoiceDate]
      ,[UnitPrice]
      ,[CustomerID]
      ,[Country]
  FROM [ONLINE RETAIIL].[dbo].[online store]
  --PRACTICE QUESTIONS
--1. Retrieve the unique countries from the invoices table.
SELECT distinct Country
FROM [ONLINE RETAIIL].[dbo].[online store]
--2. Display  the  invoice  numbers  and  quantities  of  all  items  ordered, 
--ordered by quantity in descending order.
SELECT InvoiceNo, Quantity
FROM [ONLINE RETAIIL].[dbo].[online store]
WHERE CustomerID IS NOT NULL
ORDER BY Quantity DESC;

--3. Show the top 5 most expensive items ordered by unit price.
SELECT StockCode, UnitPrice
FROM [ONLINE RETAIIL].[dbo].[online store]
ORDER BY UnitPrice desc;

--4. List the distinct stock codes along with their descriptions.
SELECT DISTINCT(StockCode), Description
FROM [ONLINE RETAIIL].[dbo].[online store]
WHERE Description IS NOT NULL
ORDER BY Description ;
--5. Select the invoice numbers, dates, and total prices (quantity  unit 
--price)  for  all  invoices,  ordered  by  the  total  price  in  descending 
--order
SELECT InvoiceNo,InvoiceDate, SUM(UnitPrice* Quantity) as total_price
FROM [ONLINE RETAIIL].[dbo].[online store]
GROUP BY InvoiceNo, InvoiceDate
ORDER by total_price DESC;

--1. How can you use the EXTRACT function to retrieve the year from 
--the "InvoiceDate" column in the "invoices" table?
----If EXTRACT is not recognized as a built-in function in your SQL environment (such as SQL Server), you can use the YEAR function instead
SELECT InvoiceNo, YEAR(InvoiceDate) AS InvoiceYear
FROM [ONLINE RETAIIL].[dbo].[online store]
--2. Write a query using the EXTRACT function to find the total 
--quantity of items sold in December 2010.

SELECT SUM(Quantity) AS TotalQuantity
FROM [ONLINE RETAIIL].[dbo].[online store]
WHERE YEAR(InvoiceDate) = 2010
  AND MONTH(InvoiceDate) = 12;
--3. How  would  you  use  the  EXTRACT  function  to  determine  the 
--number of invoices issued in January 2011?
SELECT COUNT(DISTINCT InvoiceNo) AS NO_INVOICES
FROM [ONLINE RETAIIL].[dbo].[online store]
WHERE YEAR(InvoiceDate) =2011
  AND MONTH(InvoiceDate) = 1;

--  1. MIN:-  What  is  the  minimum  unit  price  among  all  items  in  the 
--"invoices" table?
SELECT MIN(UnitPrice)
FROM [ONLINE RETAIIL].[dbo].[online store]
--2. MAX:- What is the maximum quantity of items ordered in a single 
--invoice from the "invoices" table?
SELECT MAX(Quantity)
FROM [ONLINE RETAIIL].[dbo].[online store]
--3.  AVG:- What is the average unit price of all items in the "invoices" 
--table?  
SELECT avg(UnitPrice) AS AVG_UNITPRICE
FROM [ONLINE RETAIIL].[dbo].[online store]
--4. SUM:-  What  is  the  total  quantity  of  items  ordered  across  all 
--invoices in the "invoices" table?
SELECT SUM(Quantity)
FROM [ONLINE RETAIIL].[dbo].[online store]
--5. COUNT:- How many invoices are there in the "invoices" table?
SELECT COUNT(InvoiceNo)
FROM [ONLINE RETAIIL].[dbo].[online store]
--PRACTICE QUESTIONS
--You can do it, make it happen
--1. GROUP BY:- Write a query to find the total number of invoices for 
--each customer (CustomerID) in the "invoices" table.
SELECT CustomerID, SUM(InvoiceNo)
FROM [ONLINE RETAIIL].[dbo].[online store]
where CustomerID is not null
GROUP BY CustomerID, InvoiceNo
--2. HAVING:-  How  would  you  retrieve  all  customers  (CustomerID) 
--from  the  "invoices"  table  who  have  made  purchases  with  a  total 
--quantity greater than 100?
SELECT CustomerID, Quantity
FROM [ONLINE RETAIIL].[dbo].[online store]
WHERE CustomerID IS NOT NULL
GROUP BY CustomerID, Quantity
HAVING Quantity> $100 ;

--3. GROUP BY:- Write a query to calculate the total revenue 
--(Quantity  UnitPrice) generated by each item (StockCode) sold in 
--the "invoices" table.
SELECT StockCode, SUM(Quantity*UnitPrice)
FROM [ONLINE RETAIIL].[dbo].[online store]
GROUP BY StockCode
--4. HAVING:- How would you retrieve all items (StockCode) from the 
--"invoices"  table  where  the  total  revenue  generated  is  greater 
--than $1000?
SELECT StockCode, SUM(Quantity*UnitPrice) as total_revenue
FROM [ONLINE RETAIIL].[dbo].[online store]
GROUP BY StockCode
HAVING  SUM(Quantity*UnitPrice)> $1000

