# Introduction to SQL
SQL stands for Structed Query Language. Putting a other way, it is a language to interact with a Database Server.
A database server is a software to store and manage data.
Usually a software is defined in 3 tiers: 
* Front-end (User Interface): The tier that interacts directly with the user
* Back-End (Middleware): The tier that execue the main logic of the sofware
* Database (Persitence): The tier that manager the data
  - Store
  - Protect
  - Manager
  - Retrieve
  - Create
  - Delete
  - etc

> **ATTENTION**: This material focus only in the basic concepts and try to give a quick intro to SQL

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

> **ATTENTION**: Each SQL Server has some variation of the SQL sintaxe. This material will use SQL Sintaxe for Microsoft SQL Server

> **RECOMMENDATION**: I recommend an online SQL IDE caled SQL Fiddler. You just need a browser and don't need to install anything. It supports the SQL Sintaxe for each on of the listed SQL Servers
- http://sqlfiddle.com/

# Database Organization
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
* Create table
* Insert data
* Update data
* Delete data
* Select data

# Data Modeling
Data Modeling is the process of creating an abstract representation of the information required for a system.
Data models are built around business needs and contains the data entities (Tables and Field) and their relationships.
The first step to build the Data Layer is the Data Model.

# CREATE TABLE
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

## Primary Key
A primary key is a field that uniquely identifies each record in a table.
Primary keys must contain UNIQUE values, and cannot contain NULL values.
A table can have only ONE primary key; and in the table, this primary key can consist of single or multiple columns (fields).

* Example of Primary Keys:
  - Email
  - SSN
  - EmployId
  - StudentId
  - DepartamentId

## Foreign Key
A foreign key is a field designated to store values from a field (usually a Primary Key) from another table.
The foreign key is the mechanism used in relational databases to define relationship between records.

### Example of Foreign Key
Department Table
| Departament ID | Department Name |
| --- | --- |
| 1 | Human Resources |
| 2 | Information Technology |
| 3 | Sales |
| 4 | Finances |

Employee Table
| Employee ID | Department ID | Name | Email |
| --- | --- | --- | --- |
| 1 | 2 | Jose Santos | jose.santos@noemail.com |
| 2 | 1 | Leila Rodrigues | leila.rodrigues@nomail.com |
| 3 | 2 | Artur Rodrigues | artur.rodrigues@nomail.com |
| ... |

> **ATTENTION**: Department ID is a primary key on Departament table and a foreign key on Employee table.
The departament of a Employee is defined by the value stored at his "Departament ID" field.

* Jose Santos and Artur Rodrigues are assigned to the Information Technology Departament (Departament ID = 2)
* Leila Rodrigues is assigned to the Human Resource Departament (Departament ID = 1)

## CREATE TABLE sintaxe
```sql
CREATE TABLE table_name (
    column1 datatype,
    column2 datatype,
    column3 datatype,
   ....
);
```
## CREATE TABLE example
```sql
CREATE TABLE Departament (
    ID INT PRIMARY KEY,
    Name nvarchar(100),
    Abbreviation nvarchar(5)
)

CREATE TABLE Employee (
    ID INT PRIMARY KEY,
    Name nvarchar(200),
    Email nvarchar(200),
    DepartamentID INT REFERENCES Departament(ID)
)
```

# INSERT command
The insert command is used to add records to a table

## Sintaxe
```sql
INSERT INTO table_name (column1, column2, column3, ...)
VALUES (value1, value2, value3, ...);
```

## Example
```sql
INSERT INTO Departament (ID, Name, Abbreviation) VALUES (1, 'Human Resources', 'RH')
INSERT INTO Departament (ID, Name, Abbreviation) VALUES (2, 'Information technology', 'IT')
INSERT INTO Departament (ID, Name, Abbreviation) VALUES (3, 'Sales', 'SAL')
INSERT INTO Departament (ID, Name, Abbreviation) VALUES (4, 'Finances', 'FIN')
INSERT INTO Departament (ID, Name, Abbreviation) VALUES (5, 'Marketing', 'MARK')

INSERT INTO Employee (ID, Name, Email, DepartamentID) VALUES (1, 'Jose Santos', 'jose.santos@noemail.com', 2)
INSERT INTO Employee (ID, Name, Email, DepartamentID) VALUES (2, 'Leila Rodrigues', 'leila.rodrigues@noemail.com', 1)
INSERT INTO Employee (ID, Name, Email, DepartamentID) VALUES (3, 'Artur Rodrigues', 'artur.rodrigues@noemail.com', 2)
INSERT INTO Employee (ID, Name, Email, DepartamentID) VALUES (4, 'Bob Marley', 'bob@noemail.com', 5)
INSERT INTO Employee (ID, Name, Email, DepartamentID) VALUES (5, 'Mickel Jackson', 'theking@noemail.com', 5)
INSERT INTO Employee (ID, Name, Email, DepartamentID) VALUES (6, 'Frank Sinatra', 'sinatra@noemail.com', 5)
INSERT INTO Employee (ID, Name, Email, DepartamentID) VALUES (7, 'Elon Musk', 'musk@noemail.com', 3)
INSERT INTO Employee (ID, Name, Email, DepartamentID) VALUES (8, 'Steve Jobs', 'jobs@noemail.com', 3)
INSERT INTO Employee (ID, Name, Email, DepartamentID) VALUES (9, 'Lady Gaga', 'ladygaga@noemail.com', 5)
INSERT INTO Employee (ID, Name, Email, DepartamentID) VALUES (10, 'Britney Spears', 'bspears@noemail.com', 5)
INSERT INTO Employee (ID, Name, Email, DepartamentID) VALUES (11, 'Oprah Winfrey', 'oprah@noemail.com', 5)
```

# UPDATE command
The UPDATE command is used to modify existing record(s) in a table.

** Sintaxe
```sql
UPDATE table_name
SET column1 = value1, column2 = value2, ...
[WHERE condition]
```

> **DANGER**: If you forget to use ```WHERE``` clause all the records will be updated.

## Example
```sql
update Departament
set Abbreviation = 'SA'
where ID = 3
```
* Update the Departament table, setting the Abbreviation to 'SA' for the record with ID equals to 3

# DELETE command
The DELETE statement is used to delete records from a table.

## Sitaxe
```sql
DELETE FROM table_name 
WHERE condition
```

## Example
```sql
DELETE FROM Departament WHERE ID = 4
```

> **DANGER**: If you forget to use ```WHERE``` clause all the records will be deleted.

