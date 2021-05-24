# Cosmosdb for dotnet and sql developers
This repo contains code samples and material showing how dotnet+sql developers can make the jump to CosmosDB

## How is CosmosDB different than SQL Server?
Non-relational
-Document
-Columnar
-Graph
-Key-Value

## Structure of CosmosDB

## How to transform your SQL data into CosmosDB data?

## dotnet code to  do collections and data

## EF core and Cosmos DB


## Best practices and tips


## Talk about NoSQL data storage and retrieval

## You can use SQL - show examples of SQL

Fortunately for SQL developers (and indeed for anyone with a decent grounding in SQL) the developers of Cosmos DB have spared a thought for the millions of SQL users who need a path into the brave new world of NoSQL. They have achieved this by providing an SQL API to access JSON-formatted documents stored in Cosmos DB.
However, JSON documents are far removed from relational structures and NoSQL document stores are very different beasts compared to relational databases. Consequently, the SQL used to query JSON documents is different in many ways to the conventional SQL that you use with SQL Server. Moreover, Cosmos DB SQL is severely limited compared to T-SQL Yet despite its restrictions, the Cosmos DB SQL API provides an easy path to understanding and exploiting document databases. Acquiring a working knowledge of how to query Cosmos DB could open up new horizons that enable you to integrate data from the relational and NoSQL worlds


The Basics

Cosmos DB is a multi-model NoSql database. Currently it can handle three types of non-relational data:

    Document databases
    Graph databases
    Key-value databases

Only one of these data models can be queried using SQL in Cosmos DB. This is the document database. Indeed, this is probably a good place to add that Cosmos DB SQL only concerns querying document databases. There is no DDL (data definition language) involved.


    Schema on read – Instead of the database schema being part of the database structure, any required structure is defined when the query is written.
    Nested structures – JSON documents are objects that can contain the complete data describing a self-contained unit. They can be extremely complex and represent a structure that would require a series of tables in a SQL Server database.

Basic SQL Queries
SELECT * FROM C
You will see all the documents in the current collection returned as the output

Now to be a little more selective
SELECT   saleselements.InvoiceNumber
        ,saleselements.TotalSalePrice
FROM    saleselements

Cosmos DB SQL can perform basic arithmetic:

	
SELECT   s.InvoiceNumber
         ,s.SalePrice - s.Cost AS GrossProfit
FROM     saleselements AS s

A Basic Text Filter

SELECT   s.InvoiceNumber ,s.SalePrice
FROM     s
WHERE    s.MakeName = "Bentley"

Numeric Filters

SELECT   s.InvoiceNumber ,s.SalePrice
FROM     s
WHERE    s.LineitemNumber = 2

numeric range:

	
SELECT   s.InvoiceNumber ,s.SalePrice
FROM     s
WHERE    s.Cost BETWEEN 50000 AND 100000

SELECT   s.InvoiceNumber, s.Cost BETWEEN 50000 AND 100000 
           AS InCostRange, s.SalePrice
FROM     s

Date and Time Filters

JSON does not have a date type, as such. Instead it uses a string. Consequently, you risk encountering dates in any of a myriad of formats. The upshot is that you will be delving into the specific string format to filter on dates and times.

You should endeavor to parse date time fields ISO 8601 format, which looks like this: YYYY-MM-DDTHH:MM:SS.
SELECT s.SaleDate
FROM   s
WHERE  s.SaleDate = "2015-01-02T08:00:00"

Sorting Output

Cosmos DB SQL also contains the ORDER BY clause, so you can write queries like this one:

	
SELECT   s.InvoiceNumber ,s.SalePrice AS Price
FROM     saleselements AS s
ORDER BY s.InvoiceNumber

Finding the Number of Documents in a Collection
	
SELECT VALUE COUNT(1)
FROM         s

Not recommended due to lack of schema conformity

Returning the Top N Documents
SELECT   TOP 3 s.InvoiceNumber, s.SalePrice
FROM     s
ORDER BY s.SalePrice DESC

Concatenate Attributes
 	
SELECT   CONCAT(s.CustomerName
               ," Date of Sale: "
               ,s.SaleDate) AS CustomerName
FROM     s

String Functions

SELECT   UPPER(s.CustomerName) AS CustomerName
        ,LOWER(s.CountryName) AS CountryName
        ,TRIM(s.CountryISO3) AS CountryISO3
        ,LEFT(s.MakeName, 3) AS MakeAbb
        ,RIGHT(s.InvoiceNumber, 3) AS InvoiceNumber
        ,SUBSTRING(s.InvoiceNumber, 3, 2) AS SaleCountry
FROM    s

Mathematical Functions

SELECT   ROUND(s.TotalSalePrice) AS RoundedSalePrice
        ,FLOOR(s.RepairsCost) AS RepairsCost
        ,CEILING(s.PartsCost) AS PartsCost
        ,TRUNC(s.TransportInCost) AS TransportInCost
FROM    s


## But here are some things to consider - PKs, modeling, RUs

## this is how .net developers get started

## this is how you use EF Core

## Some tips
