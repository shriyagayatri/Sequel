## *DOCUMENTATION ON ORACLE SQL*
**SQL stands for Standard Query Language. Often reffered as SEQUEL**
**SQL** is a domain-specific language used in programming and designed for managing data held in a relational database management system(RDBMS),
or for stream processing in a relational data stream management system.

### Oracle SQL Developer

![Oracle Database] (https://goo.gl/images/oD6rkb)


Oracle SQL Developer is an *Integrated development Evnvironment(IDE)* for working with SQL in Oracle database.Orcale Corporation 
provides this product free;it uses the Java Development Kit.


There are many SQL developers out there in the market but according to me the most popular ones 
in the market as of now are Microsoft SQL Server and Oracle.

We would be working on Oracle
*The main difference between these two are listed below*


### DIFFERENCE BETWEEN MICROSFT SQL SERVER AND ORACLE


![Microsoft SQL Server vs Oracle] (https://goo.gl/images/SMaQin)


* **Language** - Although both systems use a version of **Structured Query Language(SQL)**, **MS SQL Server** uses **Transant SQL**,or **T-SQL**,
           which is an extensin of SQL originally developed by *Sybase* and used by Microsoft.
           **Oracle**,on the other hand uses **PL/SQL**, or **Procedural Language/SQL**.
           *For more information about PL/SQL you can visit the following link* - <https://en.wikipedia.org/wiki/PL/SQL>
      
* **Transaction Control** - A transaction can be defined as a group of operations or tasks that should be treated as a single unit.
                      By default, **MS SQL Server** will execute and commit each command/task individually, and it will be difficult
                       or impossible to roll back changes if any errors are encountered along the way. 
                      Within **Oracle**, on the other hand, each new database connection is treated as new transaction. As queries are
                      executed and commands are issued, changes are made only in memory and nothing is committed until an explicit  
                      COMMIT statement is given (with a few exceptions related to DDL commands which include “implicit” commits,
                      and are committed immediately). After the COMMIT, the next command issued essentially initiates a new
                      transaction, and the process begins again. This provides greater flexibility and helps for error control as 
                      well, as no changes are committed to disk until the DBA explicitly issues the command to do so.
                     
* **Organization of Database Objects** - **MS SQL Server** organizes all objects, such as tables, views, and procedures, by database *names*.
                                   Users are assigned to a login which is granted accesses to the specific database and its objects. 
                                   Also, in SQL Server each database has a private, unshared disk file on the server. In *Oracle*, 
                                   all the database objects are grouped by *schemas*, which are a subset collection of database 
                                   objects and all the database objects are shared among all schemas and users. Even though it 
                                   is all shared, each user can be limited to certain schemas and tables via roles and permissions.

                     
           

