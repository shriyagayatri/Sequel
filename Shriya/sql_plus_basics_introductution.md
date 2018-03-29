# STARTING SQLPLUS

To start SQLPLUS following command is used


**$SQLPLUS**
[$-Operator System Command prompt]


> SPOOL OP_TXT
  SELECT * 
 FROM company;
  *SPOOL OFF;*

Here,the output of the query SELECT * FROM COMPANY goes to the file OP_TXT . to close the file,
the command **SPOOL OFF** is used . By default spool file has the extension *.LST* . So the file created,
in this case,will be * OP_TXT.LST * present in the bin directory.


### COMMAND FOR CREATING TABLE

 **CREATE TABLE <table name> (<column1><type>, <column2><type>,....);**
  
  

> Example:
        CREATE TABLE emp_company
        (ename varchar2 (10),cname varchar2 (10),salary number (7,2),jdate date);

### DESCRIBE COMMAND

**DESCRIBE emp_company;**







### INSERTING DATA IN TABLE

 **INSERT [into] {table_name} [(coloumn_list) **
  **VALUES (expression [ ,...n]);**

> Example:
        INSERT INTO company VALUES ('acc','bombay');

*To change the order in which data is inserted it should be specified explicitly*

> Example:
        INSERT INTO company(city,cname)
        VALUES ('bombay','acc');

**//Using Substitution Variable**

**INSERT INTO company 
  VALUES (&cname,&city);**           *[& indicates substitution values]*

[The statement prompts the value of cname and city]

Result:
       Enter the value of cname: 'acc'
       Enter the value of city: 'nagpur'

Enter the above value and press enter, a message will popup stating 'row created'.
anothe rrecord can be inserted in the same table just by typing **'RUN'** at the SQL prompt.

**RUN;**
  (or)
  **SQL>/**

**NOTE-The combination of RUN and & can be used for fast insertion**

### SELECT STATEMENT WITH CONDITION

 **SELECT col1,col2**
  **FROM t1,t2....**
  **WHERE<condition>;** 

> NOTE-The WHERE condition should be a bolean expression that returns true or false.
   Multilpe conditions can be combined using AND,OR and NOT operators. **

>  NOTE- SELECT cname company name FROM company;
      is same as   
      SELECT cname AS companyname FROM company; **

### USING TABLE ALIAS

**TABLENAME.COLOUMNNAME [IF ALIAS IS NOT MENTIONED]
  ALIASNAME.COLOUMNNAME [IF ALIAS IS MENTIONED]**

> EXAMPLE-
        SELECT c1.cname AS companyname
        FROM company c1;                 [here c1 is table alias]

### Retrieving values of system variable in SQL format

 **SELECT SYSDATE
  FROM DUAL;**

RESULT-
       SYSDATE
       --------
       18-MARCH-18

### Evaluating expression in SQL

 **SELECT 3*4+2
  FROM DUAL;**

RESULT-
       3*4+2
       ------
           14

### EXAMPLES TO SHOW THE USE OF CONDITIONS

1. > #### AND condition
   SELECT ename
   FROM emp_company
   WHERE cname = 'acc' AND salary>1000;

2. > #### NOT condition
   SELECT ename
   FROM emp_c
   WHERE NOT (ename='acc');
Alternatively,
   SELECT ename
   FROM emp_company
   WHERE cname<>'acc';

3. > #### OR condition
   SELECT ename
   FROM emp_company
   WHERE cname ='acc' OR cname = 'tata';


Oracle recommends using LOB datatype instead of LONG datatype. Maximum of one LONG coloumn can be 
specified in one table.LONG coloumn can appear only in SET clause of UPDATE statement,INSERT statement
 and SELECT clause.LONG coloumn cannot be used in other clauses,such as WHERE clause.
 
 
 ## SET OPERATIONS 

1. ### UNION OPERATION

> Example-
        SELECT city 
        FROM company
        WHERE cname = 'acc'
        UNION
        SELECT city 
        FROM company
        WHERE cname = 'tata';


> SELECT cname,city
FROM company
WHERE cname = 'acc'
UNION
SELECT city
FROM company
WHERE cname ='tata';

The above statement can't be written because the first set produces two parts,while the second set has an element with single part.

In such cases a dummy coloumn can be created

> SELECT cname,city
FROM company
WHERE cname = 'acc'
UNION
SELECT '',city              //creating dummy variable
FROM company
WHERE cname = 'tata';


2. ### INTERSECT OPERATION

> Example-
        SELECT city
        FROM company
        WHERE cname = 'acc'
        INTERSECT
        SELECT city
        FROM company
        WHERE cname = 'tata';


3. ### MINUS OPERATION

> SELECT city
FROM company
WHERE cname = 'acc'
MINUS
SELECT city
FROM company
WHERE cname = 'tata';

4. ### IN CLAUSE

SELECT ename,city
FROM employee
WHERE ename IN(SELECT ename FROM emp_company WHERE cname = 'acc');

> IN CLAUSE can only be used in 'where' condition and it returns TRUE or FALSE.


5. ### EXISTS CLAUSE

The exists clause is used for testing whether a given set is empty or not .It is used in WHERE condition.
Exists clause of an empty set returns  FALSE,while an nonempty set returns TRUE

> Example-
        EXISTS {a,b,c,d} = true
        AND
        EXISTS {} = false
        
   ## AGGREGATE FUNCTIONS

Aggregate functions are used for performing group operations.

> Example-
        SELECT MAX(salary)
        FROM emp_company;

NOTE- Other aggregate functions are mip,sum,avg,count and stdev(standard deviation).

> Example-
        SELECT MAX(salary)
        FROM emp_company
        WHERE cname = 'acc';




### HAVING CLAUSE

> SELECT cname,COUNT(ename)
FROM emp_company 
GROUP BY cname
HAVING count(ename) > 1;

Here,groups are formed on cname and then,for each group,rows with having condition are evaluated.The
rows that satisfy having condition are displayed.


### WITH CLAUSE

> WITH companysalary 
AS( SELECT cname, SUM(salary) totalsal
FROM emp_company GROUP BY cname),
companyAVGsalary AS(SELECT AVG(TOTALsal) AVGsal FROM companysalary)
SELECT cname,totalsal
FROM companysalary
WHERE totalsal > (SELECT AVGsal FROM companyavgsalary);



### ORDER BY CLAUSE

> SELECT ename,cname
FROM emp_company
ORDER BY 1;

NOTE- 1 means first coloumn in select clause


SELECT ename,cname
FROM emp_company
ORDER BY 1 DEC;


## UPDATING AND DELETING DATA IN EXISTING TABLE (DML)

### THE UPDATE STATEMENT

> UPDATE<table name>
SET column1= ,column2..........
WHERE <condition>

> NOTE-Only one table name can be used with update statement

Example-
        UPDATE emp_company
        SET salary = salary * 0.2

In case the user wants to specifya condition with respect to two or more tables then it can be done using an **in** or **exists** clause

> Example-
        UPDATE emp_company SET salary = salary + 100
        WHERE ename ='sunil' AND cname = 'acc'
        AND EXISTS (SELECT e1. ename FROM emp_company e1 WHERE
        e1.ename = 'anil' AND e1. cname = 'acc');

### THE DELETE STATEMENT

Delete statement detels rows not the entire table

> Example-
        DELETE employee
        WHERE city = 'chennai';   //This deletes all the rows of the table



### DROPPING THE TABLE

This delets entire table

> DROP TABLE employee;


### INSERTING DATA USING QUERY

INSERT INTO employee (ename,city)
SELECT e1.ename, c2.city
FROM emp_company e1,company c2
WHERE
e1.cname = 'acc'
AND e1.cname= c2.cname;








