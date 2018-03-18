# STARTING SQLPLUS

To start SQLPLUS following command is used

** $SQLPLUS **
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



