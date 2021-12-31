# Introduction to SQL
SQL stands for Structured Query Language. Put differently, it is a language to interact with a Database Server.
A database server is a software to store and manage data.

Usually, a System/Application is devided in 3 tiers: 
* Front-end (User Interface): The tier that interacts with the user
* Back-End (Middleware): The tier that executes the main logic of the System
* Database (Persistence): The tier that manages the data
  - Store
  - Protect
  - Manager
  - Retrieve
  - Create
  - Delete
  - etc

# Some Context
SQL is usually related to Relational Databases. There are many different types of databases and in general, all database types that are not relational are called NoSQL DATABASE. A quick search and you will find a long list of SQL and NoSQL databases servers. Each database technology is specialized in something. So there is no such thing as the best database technology for all situations.

# Practices
There are several free SQL Server and IDEs that you can use to practice:
* SQL Lite
  - https://www.sqlite.org
* MYSQL
  - https://www.mysql.com
* Postgre SQL
  - https://www.postgresql.org
* Microsoft SQL Server Express (The free version of Microsoft SQL Server)
  - https://www.microsoft.com/en-us/download/details.aspx?id=101064

> **ATTENTION**: 
  * Each SQL Server has some variation of the SQL syntax. 
  * This material will use SQL Syntax for MySQL. 
  * This material focuses only on the basic concepts and tries to give a quick intro to SQL.

> **RECOMMENDATION**: I recommend an online SQL IDE called SQL Fiddler. You just need a browser and don't need to install anything. It supports the SQL Syntax for each one of the listed SQL Servers
- http://sqlfiddle.com/

# Database Organization
* A relational database organizes the information in tables and fields.
* A table is an entity to store data.
  * Examples: 
     * Customer
     * Product
     * Employee
     * Project

* A field is a unit of data that compose a Table.
  * Examples:
    * ID
    * first_name
    * last_name
    * email
    * salary

* A record is a row (instance) of data in a table:
  * Example of a Row:

| ID | first_name | last_name | email | salary |
| --- | --- | --- | --- | --- |
| 1 | Jose | Santos | airamez@gmail.com | 150,000.00|

# Operations
SQL defines a sitaxe to execute commands to:
* Create table
* Insert data
* Update data
* Delete data
* Select data

# Data Modeling
Data Modeling is the process of creating an abstract representation of the information required for a system.
Data models are built around business needs and contain the data entities (Tables and Field) and their relationships.
The first step to build the Data Layer is the Data Model.

> **WARNING**: SQL Server commands are not case sensitive. This material will use Upper case just to help with visualization

# CREATE TABLE
A table is defined by a list of fields and before we create a table it is important to understand the field types (DataType).

## Fields Data Types
> **ATTENTION**: This is not a full list of data types but the most common ones |

Full list: https://dev.mysql.com/doc/refman/8.0/en/data-types.html

* Numerics (https://dev.mysql.com/doc/refman/8.0/en/numeric-types.html): 
  * INTEGER
  * SMALLINT
  * DECIMAL
  * NUMERIC
* Date and Time (https://dev.mysql.com/doc/refman/8.0/en/date-and-time-types.html)
  * DATE
  * TIME
  * DATETIME
  * TIMESTAMP
  * YEAR
* String (https://dev.mysql.com/doc/refman/8.0/en/string-types.html)
  * CHAR
  * VARCHAR
  * BINARY
  * VARBINARY
  * BLOB
  * TEXT
  * ENUM
  * SET
* JSON (https://dev.mysql.com/doc/refman/8.0/en/json.html)

## Primary Key
A primary key is a field that uniquely identifies each record in a table.
Primary keys must contain UNIQUE values, and cannot contain NULL values.
A table can have only ONE primary key; and in the table, this primary key can consist of single or multiple columns (fields).
> **ATTENTION**: Most of the time the Primary Key is auto generated value |

* Example of Primary Keys:
  * Email
  * SSN
  * EmployId
  * StudentId
  * DepartmentId

## Foreign Key
A foreign key is a field designated to store values from a field (usually a Primary Key) from another table.
The foreign key is the mechanism used in relational databases to define relationships between records.

### Example of Foreign Key
Department Table
| Department ID | Department Name |
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

> **ATTENTION**: Department ID is a primary key on the Department table and a foreign key on the Employee table.
The department of an Employee is defined by the value stored at his "Department ID" field.

* Jose Santos and Artur Rodrigues are assigned to the Information Technology Department (Department ID = 2)
* Leila Rodrigues is assigned to the Human Resource Department (Department ID = 1)

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
CREATE TABLE Department (
    ID INT NOT NULL AUTO_INCREMENT,
    Name varchar(100),
    Abbreviation varchar(5),
    PRIMARY KEY (ID)
);

CREATE TABLE Employee (
    ID INT NOT NULL AUTO_INCREMENT,
    Name varchar(200),
    Email varchar(200),
    Salary DECIMAL(13,2),
    DepartmentID INT,
    PRIMARY KEY (ID),
    FOREIGN KEY (DepartmentID) REFERENCES Department(ID)
)
```
> **WARNING**: When executing multiple SQL statements, it is necessary to finish each one ';'.

# INSERT command
The insert command is used to add records to a table

## Sintaxe
```sql
INSERT INTO table_name (column1, column2, column3, ...)
VALUES (value1, value2, value3, ...);
```

## Example
```sql
INSERT INTO Department (Name, Abbreviation) VALUES ('Human Resources', 'HR');
INSERT INTO Department (Name, Abbreviation) VALUES ('Information Technology', 'IT');
INSERT INTO Department (Name, Abbreviation) VALUES ('Sales', 'SAL');
INSERT INTO Department (Name, Abbreviation) VALUES ('Finances', 'FIN');
INSERT INTO Department (Name, Abbreviation) VALUES ('Marketing', 'MARK');
INSERT INTO Department (Name, Abbreviation) VALUES ('Public Relations', 'PL');

INSERT INTO Employee (Name, Email, Salary, DepartmentID) VALUES
('Jose Santos', 'jose.santos@noemail.com', 15000.15, 2),
('Leila Rodrigues', 'leila.rodrigues@noemail.com', 200000.20, 1),
('Artur Rodrigues', 'artur.rodrigues@noemail.com', 100000.45, 2),
('Bob Marley', 'bob@noemail.com', 900000.37, 5),
('Mickael Jackson', 'theking@noemail.com', 2000000.00, 5),
('Frank Sinatra', 'sinatra@noemail.com', 700000.67, 5),
('Elon Musk', 'musk@noemail.com', 450000.15, 3),
('Steve Jobs', 'jobs@noemail.com', 1000000.67, 3),
('Lady Gaga', 'ladygaga@noemail.com', 650000.90, 5),
('Britney Spears', 'bspears@noemail.com', 75000.56, 5),
('Oprah Winfrey', 'oprah@noemail.com', 5000000.01,5);
```
> **ATTENTION**: No need to insert the ID field because it is auto-gerenated (AUTO_INCREMENT)

> **TIP**: It is possible to insert multiple rows with just one INSERT command. Check the INSERT command on Employee table

# UPDATE command
The UPDATE command is used to modify existing record(s) in a table.

## Sintaxe
```sql
UPDATE table_name
SET column1 = value1, column2 = value2, ...
[WHERE condition]
```

> **DANGER**: If you forget to use the ```WHERE``` clause all the records will be updated.

## Example
```sql
UPDATE Department
SET Abbreviation = 'SA'
WHERE ID = 3
```
* Update the Department table, setting the Abbreviation to 'SA' for the record with ID equals 3

# DELETE command
The DELETE statement is used to delete records from a table.

## Sitaxe
```sql
DELETE FROM table_name 
WHERE condition
```
> **DANGER**: If you forget to use the ```WHERE``` clause all the records will be deleted.

## Example
```sql
DELETE FROM Department WHERE ID = 4
```
* The row with ID equals 4 will be deleted from the Department table

# Preparation for the SELECT command examples
* These are the SQL commands to prepare the database for the select examples
* Execute the commands below into your sandbox database to create the tables and insert records necessary for the following examples
* If you are using SQL Fiddler, execute these commands on the left side (Build Schema Section) and execute the examples on the right side.

```sql
CREATE TABLE Department (
    ID INT NOT NULL AUTO_INCREMENT,
    Name varchar(100),
    Abbreviation varchar(5),
    PRIMARY KEY (ID)
);

CREATE TABLE Employee (
    ID INT NOT NULL AUTO_INCREMENT,
    Name varchar(200),
    Email varchar(200),
    DepartmentID INT,
    PRIMARY KEY (ID),
    FOREIGN KEY (DepartmentID) REFERENCES Department(ID)
);

INSERT INTO Department (Name, Abbreviation) VALUES ('Human Resources', 'HR');
INSERT INTO Department (Name, Abbreviation) VALUES ('Information Technology', 'IT');
INSERT INTO Department (Name, Abbreviation) VALUES ('Sales', 'SAL');
INSERT INTO Department (Name, Abbreviation) VALUES ('Finances', 'FIN');
INSERT INTO Department (Name, Abbreviation) VALUES ('Marketing', 'MARK');
INSERT INTO Department (Name, Abbreviation) VALUES ('Public Relations', 'PL');

INSERT INTO Employee (Name, Email, Salary, DepartmentID) VALUES
('Jose Santos', 'jose.santos@noemail.com', 15000.15, 2),
('Leila Rodrigues', 'leila.rodrigues@noemail.com', 200000.20, 1),
('Artur Rodrigues', 'artur.rodrigues@noemail.com', 100000.45, 2),
('Bob Marley', 'bob@noemail.com', 900000.37, 5),
('Mickael Jackson', 'theking@noemail.com', 2000000.00, 5),
('Frank Sinatra', 'sinatra@noemail.com', 700000.67, 5),
('Elon Musk', 'musk@noemail.com', 450000.15, 3),
('Steve Jobs', 'jobs@noemail.com', 1000000.67, 3),
('Lady Gaga', 'ladygaga@noemail.com', 650000.90, 5),
('Britney Spears', 'bspears@noemail.com', 75000.56, 5),
('Oprah Winfrey', 'oprah@noemail.com', 5000000.01,5);
```

# SELECT command
The SELECT command is used to select/retrieve data from a database.

## Sintaxe
```sql
SELECT * FROM table_name;

SELECT column1, column2, ...
FROM table_name;
WHERE condition
```

> **TIP**: Using ```SELECT *``` is not recommended as we rarely need all fields. It is better to use a list with only the necessary fields.

## Select all columns and all rows from Employee table
```sql
SELECT * FROM Employee
```
### Result
    | ID |            Name |                       Email |     Salary | DepartmentID |
    |----|-----------------|-----------------------------|------------|--------------|
    |  1 |     Jose Santos |     jose.santos@noemail.com |   15000.15 |            2 |
    |  2 | Leila Rodrigues | leila.rodrigues@noemail.com |   200000.2 |            1 |
    |  3 | Artur Rodrigues | artur.rodrigues@noemail.com |  100000.45 |            2 |
    |  4 |      Bob Marley |             bob@noemail.com |  900000.37 |            5 |
    |  5 | Mickael Jackson |         theking@noemail.com |    2000000 |            5 |
    |  6 |   Frank Sinatra |         sinatra@noemail.com |  700000.67 |            5 |
    |  7 |       Elon Musk |            musk@noemail.com |  450000.15 |            3 |
    |  8 |      Steve Jobs |            jobs@noemail.com | 1000000.67 |            3 |
    |  9 |       Lady Gaga |        ladygaga@noemail.com |   650000.9 |            5 |
    | 10 |  Britney Spears |         bspears@noemail.com |   75000.56 |            5 |
    | 11 |   Oprah Winfrey |           oprah@noemail.com | 5000000.01 |            5 |

## Select only ID and Name fields from the Employee table
```sql
SELECT ID, Name, Salary FROM Employee
```
### Result
    | ID |            Name |     Salary |
    |----|-----------------|------------|
    |  1 |     Jose Santos |   15000.15 |
    |  2 | Leila Rodrigues |   200000.2 |
    |  3 | Artur Rodrigues |  100000.45 |
    |  4 |      Bob Marley |  900000.37 |
    |  5 | Mickael Jackson |    2000000 |
    |  6 |   Frank Sinatra |  700000.67 |
    |  7 |       Elon Musk |  450000.15 |
    |  8 |      Steve Jobs | 1000000.67 |
    |  9 |       Lady Gaga |   650000.9 |
    | 10 |  Britney Spears |   75000.56 |
    | 11 |   Oprah Winfrey | 5000000.01 |

## Select all fields from employee where the Department ID equals 5
```sql
SELECT * FROM Employee
WHERE DepartmentID = 5
```
### Result
    | ID |            Name |                Email |     Salary | DepartmentID |
    |----|-----------------|----------------------|------------|--------------|
    |  4 |      Bob Marley |      bob@noemail.com |  900000.37 |            5 |
    |  5 | Mickael Jackson |  theking@noemail.com |    2000000 |            5 |
    |  6 |   Frank Sinatra |  sinatra@noemail.com |  700000.67 |            5 |
    |  9 |       Lady Gaga | ladygaga@noemail.com |   650000.9 |            5 |
    | 10 |  Britney Spears |  bspears@noemail.com |   75000.56 |            5 |
    | 11 |   Oprah Winfrey |    oprah@noemail.com | 5000000.01 |            5 |

## Select the Email field of all Employees of the IT and HR departments
```sql
SELECT Email FROM Employee
WHERE DepartmentID = 1 OR DepartmentID = 2
```
### Result
    |                       Email |
    |-----------------------------|
    |     jose.santos@noemail.com |
    | leila.rodrigues@noemail.com |
    | artur.rodrigues@noemail.com |

## Select all columns from Employee and Department tables
* To select fields from two or more tables it is necessary to make a relational operation called JOIN
* A join operation uses foreign keys to relate the records
* As the Employee table has a foreign key (Department ID) from Department (ID), the select command can join the related records from both tables
* The rows on the result dataset will be mapped (linked) based on the combination of Department ID on Employee table and ID on Department table.
* In a join operation is necessary to use alias, identifiers right after the table name, to distinguish fields from different tables.
```sql
SELECT * 
FROM Employee e
JOIN Department d on d.ID = e.DepartmentID
```

### Result
    | ID |            Name |                       Email |     Salary | DepartmentID | ID |                   Name | Abbreviation |
    |----|-----------------|-----------------------------|------------|--------------|----|------------------------|--------------|
    |  2 | Leila Rodrigues | leila.rodrigues@noemail.com |   200000.2 |            1 |  1 |        Human Resources |           HR |
    |  1 |     Jose Santos |     jose.santos@noemail.com |   15000.15 |            2 |  2 | Information Technology |           IT |
    |  3 | Artur Rodrigues | artur.rodrigues@noemail.com |  100000.45 |            2 |  2 | Information Technology |           IT |
    |  7 |       Elon Musk |            musk@noemail.com |  450000.15 |            3 |  3 |                  Sales |          SAL |
    |  8 |      Steve Jobs |            jobs@noemail.com | 1000000.67 |            3 |  3 |                  Sales |          SAL |
    |  4 |      Bob Marley |             bob@noemail.com |  900000.37 |            5 |  5 |              Marketing |         MARK |
    |  5 | Mickael Jackson |         theking@noemail.com |    2000000 |            5 |  5 |              Marketing |         MARK |
    |  6 |   Frank Sinatra |         sinatra@noemail.com |  700000.67 |            5 |  5 |              Marketing |         MARK |
    |  9 |       Lady Gaga |        ladygaga@noemail.com |   650000.9 |            5 |  5 |              Marketing |         MARK |
    | 10 |  Britney Spears |         bspears@noemail.com |   75000.56 |            5 |  5 |              Marketing |         MARK |
    | 11 |   Oprah Winfrey |           oprah@noemail.com | 5000000.01 |            5 |  5 |              Marketing |         MARK |

## Select 'Employee Name' and 'Department Name' fields from Employee and Department tables
```sql
SELECT e.Name, d.Name
FROM Employee e
JOIN Department d on d.ID = e.DepartmentID
```
### Result
    |            Name |                   Name |
    |-----------------|------------------------|
    | Leila Rodrigues |        Human Resources |
    |     Jose Santos | Information Technology |
    | Artur Rodrigues | Information Technology |
    |       Elon Musk |                  Sales |
    |      Steve Jobs |                  Sales |
    |      Bob Marley |              Marketing |
    | Mickael Jackson |              Marketing |
    |   Frank Sinatra |              Marketing |
    |       Lady Gaga |              Marketing |
    |  Britney Spears |              Marketing |
    |   Oprah Winfrey |              Marketing |

## Select 'Employee Name' and 'Department Name' fields but renaming them to 'Employee Name' and 'Department Name' respectively
```sql
SELECT e.Name as 'Employee Name', 
       d.Name as 'Department Name'
FROM Employee e
JOIN Department d on d.ID = e.DepartmentID
```
### Result
    |   Employee Name |        Department Name |
    |-----------------|------------------------|
    | Leila Rodrigues |        Human Resources |
    |     Jose Santos | Information Technology |
    | Artur Rodrigues | Information Technology |
    |       Elon Musk |                  Sales |
    |      Steve Jobs |                  Sales |
    |      Bob Marley |              Marketing |
    | Mickael Jackson |              Marketing |
    |   Frank Sinatra |              Marketing |
    |       Lady Gaga |              Marketing |
    |  Britney Spears |              Marketing |
    |   Oprah Winfrey |              Marketing |

## Sorting Data, Select 'Employee Name' and 'Department Name' fields from Employee and Department tables
```sql
SELECT d.Name as 'Department Name',
       e.Name as 'Employee Name'
FROM Employee e
JOIN Department d on d.ID = e.DepartmentID
ORDER BY d.Name, e.Name
```
* Sorting by Department and Employee Names
### Result
   |        Department Name |   Employee Name |
    |------------------------|-----------------|
    |        Human Resources | Leila Rodrigues |
    | Information Technology | Artur Rodrigues |
    | Information Technology |     Jose Santos |
    |              Marketing |      Bob Marley |
    |              Marketing |  Britney Spears |
    |              Marketing |   Frank Sinatra |
    |              Marketing |       Lady Gaga |
    |              Marketing | Mickael Jackson |
    |              Marketing |   Oprah Winfrey |
    |                  Sales |       Elon Musk |
    |                  Sales |      Steve Jobs |

## LEFT or RIGHT JOIN
The default behavior of a join command (INNER JOIN) is to return only rows with data from both tables.
If it is necessary to return data from one of the tables even if there is no foreign key mapping, it is necessary to use LEFT or RIGHT join. The table in the ```FROM``` clause is the LEFT one and the table in the ```JOIN``` clause is the RIGHT one.
```sql
SELECT e.Name as 'Employee Name', 
       d.Name as 'Department Name'
FROM Employee e
RIGHT JOIN Department d on d.ID = e.DepartmentID
```
### Result
    |   Employee Name |        Department Name |
    |-----------------|------------------------|
    | Leila Rodrigues |        Human Resources |
    |     Jose Santos | Information Technology |
    | Artur Rodrigues | Information Technology |
    |       Elon Musk |                  Sales |
    |      Steve Jobs |                  Sales |
    |          (null) |               Finances |
    |      Bob Marley |              Marketing |
    | Mickael Jackson |              Marketing |
    |   Frank Sinatra |              Marketing |
    |       Lady Gaga |              Marketing |
    |  Britney Spears |              Marketing |
    |   Oprah Winfrey |              Marketing |
    |          (null) |       Public Relations |

* ```Employee``` is LEFT and ```Department`` is RIGHT
* Compare this result to the one from the previous example and observe that this one has two extra rows with no Employee Name for Finance Department and Public Relations.
* As there is no Employee with a Department ID equal to 4 or 5, it is necessary a RIGHT JOIN to retrieve a row for each one of those departments.

## MAX, MIN, SUM and AVG
  * MAX returns the maximum value of a field
  * MIN returns the minimum value of a field
  * SUM returns the sum of all values of a field
  * AVG returns the average value of a field
```sql
SELECT MIN(Salary) as 'Minimum',
       MAX(Salary) as 'Maximum',
       SUM(Salary) as 'Sum',
       AVG(Salary) as 'Average'
FROM Employee
```

### Result
    |  Minimum |    Maximum |         Sum |        Average |
    |----------|------------|-------------|----------------|
    | 15000.15 | 5000000.01 | 11090004.13 | 1008182.193636 |

## COUNT
* The COUNT clause returns the number of the records in the dataset (result of the SELECT command)

```
SELECT COUNT(ID) as 'Employee COUNT'
FROM Employee
WHERE DepartmentID = 5
```
### Result
    | Employee COUNT |
    |----------------|
    |              6 |

## GROUP BY and COUNT
* It is possible to group the information based on a field and use a COUNT command
* The command below return a list with the Department name and the number of Employees associated with the Department
```sql
SELECT d.Name, COUNT(e.ID) as 'Employee Count'
FROM Department d
JOIN Employee e on e.DepartmentID = d.ID
GROUP BY d.Name
ORDER BY d.Name
```
### Result
    |                   Name | Employee Count |
    |------------------------|----------------|
    |        Human Resources |              1 |
    | Information Technology |              2 |
    |              Marketing |              6 |
    |                  Sales |              2 |

## GROUP BY and COUNT with LEFT JOIN
* It is possible to group the information based on a field and use a COUNT command
* The command below return a list with the Department name and the number of Employees associated with the Department
```sql
SELECT d.Name, COUNT(e.ID) as 'Employee Count'
FROM Department d
LEFT JOIN Employee e on e.DepartmentID = d.ID
GROUP BY d.Name
ORDER BY d.Name
```
### Result
    |                   Name | Employee Count |
    |------------------------|----------------|
    |               Finances |              0 |
    |        Human Resources |              1 |
    | Information Technology |              2 |
    |              Marketing |              6 |
    |       Public Relations |              0 |
    |                  Sales |              2 |

> **ATTENTION**: Using the left join makes sure the departments without Employees are returned.