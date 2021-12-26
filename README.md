# Introduction to SQL
SQL stands for Structed Query Language. Putting a other way, it is a language to interact with a Database Server.
A database server is a software to store and manage data.
Usually a software is defined in 3 tiers: 
* Front-end: The tier that interacts directly with the user
* Back-End: The tier that execue the main logic of the sofware
* Database: The tier that manager the data
  - Store
  - Protect
  - Manager
  - Retrieve
  - Create
  - Delete
  - etc

# Some Context
SQL is usually related to Relational Databases. There are many different types of database and in general all database types that are not relational are called NO-SQL DATABASE. A quick search and you will find a long list of them and each one specialized in something. So there is no such thing is the best database technology as each on is best for different needs.
It is a disater try to use a database technology to do something that it is not best design for.

# Practice
There are several free SQL Server that you can use to practice
* SQL Lite
  - https://www.sqlite.org
* MYSQL
  - https://www.mysql.com
* Postgre SQL
  - https://www.postgresql.org
* Microsoft SQL Server Express (The free version of Microsoft SQL Server)
  - https://www.microsoft.com/en-us/download/details.aspx?id=101064

> **ATTENTION**: Each SQL Server has some variation of the SQL sintaxe. This material will use SQL Sintaxe for Microsoft SQL Server |

I recommend an online SQL IDE caled SQL Fiddler. You just need a browser and don't need to install anything. It supports the SQL Sintaxe for each on of the listed SQL Servers
- http://sqlfiddle.com/

# Organization
* A relational database organizes the information in tables and fields.
* A table is a entity to store data.
  - Table Examples: Customer, Product, Employee, Project, etc

* A field is a unit of data that compose a Table.
  - Fields Example: ID, first_name, last_name, email, salary, etc.

* A record is a row (instance) of data in a table:
  - Example of a Row:

| ID | first_name | last_name | email | salary |
| --- | --- | --- | --- | --- |
| 1 | Jose | Santos | airamez@gmail.com | 150,000.00|

# Operations
SQL define a sitaxe to execute commands to:
* Create Table
* Select Data
* Update Data
* Delete Data

# Create Table
A table is define by a list of field and before we create a table it is important to understand the field types (Data Type).

## Fields Data Types
> **ATTENTION**: This is not a full list of data types but the most common ones |

* INT: 
  - Integer number
  - 4 bytes
  - Range: -2^31 (-2,147,483,648) to 2^31-1 (2,147,483,647)
* NUMERIC
  - Decimal number
  - Numeric is define by two part: precision and scale
    -- Precision: The max number of digits
    -- Scale: The max number of decimal digits
* MONEY
  - Money
  - 8 bytes
  - Range: -922,337,203,685,477.5808 to 922,337,203,685,477.5807
* DATETIME2
  - Date and Time
  - Range: January 1,1 CE through December 31, 9999 CE
* VARCHAR
  - Strings as ASCII
* NVARCHAR
  - Strings as UNICODE

## Create table command
```sql
CREATE TABLE table_name (
    column1 datatype,
    column2 datatype,
    column3 datatype,
   ....
);
```

