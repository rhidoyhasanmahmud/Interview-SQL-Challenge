### Things To Know

- SQL stands for Structured Query Language. It’s a standard language for accessing and manipulating databases.
- MySQL is a database management system, like SQL Server, Oracle, Informix, Postgres, etc.
- MySQL is a RDMS (Relational Database Management System).

MS SQL : Microsoft’s Implementation of SQL

Oracle SQL : Oracle's Implementation of SQL

MySQL : Sun Systems Implementation of SQL (Open Source) later on supported by Oracle Corporation.

PostgreSQL : Another open source Implementation.

There are many others from other vendors too. DB2 -IBM, Sybase, Ingress, Informix etc.,

### How does an SQL query work?

SQL execution order:

FROM -> WHERE -> GROUP BY -> HAVING -> SELECT -> DISTINCT -> ORDER BY -> LIMIT .

SQL Query mainly works in three phases .

1) Row filtering - Phase 1: Row filtering - phase 1 are done by FROM, WHERE , GROUP BY , HAVING clause.

2) Column filtering: Columns are filtered by SELECT clause.

3) Row filtering - Phase 2: Row filtering - phase 2 are done by DISTINCT , ORDER BY , LIMIT clause.

In here i will explain with an example . Suppose we have a students table as follows:

| id_	| name_	| marks	| section |
| ------------ |---------------| -----|-------|
|1|	Julia	|88|	A|
|2|	Samantha|	68	|B|
|3|	Maria	|10|	C|
|4|	Scarlet	|78	|A|
|5|	Ashley	|63|	B|
|6|	Abir|	95|	D|
|7|	Jane|	81|	A|
|8|	Jahid|	25|	C|
|9|	Sohel|	90|	D|
|10|	Rahim	|80|	A|
|11|	Karim	|81	|B|
|12|	Abdullah	|92	|D|

Now we run the following sql query:
> select section_,sum(marks) from students where id_<10 GROUP BY section_ having sum(marks)>100 order by section_ LIMIT 2;

Output of the query is:

|section_|	sum|
|----|------|
|A|	247|
|B|	131|

But how we got this output ?

I have explained the query step by step . Please read bellow:

1. FROM , WHERE clause execution 
   
Hence, from clause works first therefore from students where id_<10 query will eliminate rows which has id_ greater than or equal to 10 . So the following rows remains after executing from students where id_<10 .

|id_|	name_|	marks|	section|
|-----|----|----|----|
|1|	Julia	|88	|A|
|2|	Samantha	|68|	B
|3|	Maria	|10	|C|
|4|	Scarlet	|78	|A|
|5|	Ashley	|63	|B|
|6|	Abir	|95	|D|
|7|	Jane	|81	|A|
|8|	Jahid	|25	|C|
|9|	Sohel	|90	|D |  

2. GROUP BY clause execution 
   
Now GROUP BY clause will come , that's why after executing GROUP BY section_ rows will make group like bellow:

|id_|	name_|	marks|	section|
|-----|----|----|----|
|9|	Sohel	|90	|D|
|6|	Abir	|95	|D|
|1|	Julia	|88	|A|
|4|	Scarlet	|78	|A|
|7|	Jane	|81	|A|
|2|	Samantha|	68|	B|
|5|	Ashley	|63|	B|
|3|	Maria	|10|	C|
|8|	Jahid	|25|	C|

3. HAVING clause execution
   
Having sum(marks)>100 will eliminate groups . sum(marks) of D group is 185 , sum(marks) of A groupd is 247 , sum(marks) of B group is 131 , sum(marks) of C group is 35 . So we can see tha C groups's sum is not greater than 100 . So group C will be eliminated . So the table looks like this:

|id_|	name_|	marks|	section|
|-----|----|----|----|
|9|	Sohel	|90|	D|
|6|	Abir	|95	|D|
|1|	Julia	|88|	A|
|4|	Scarlet	|78	|A|
|7|	Jane	|81|	A|
|2|	Samantha|	68	|B|
|5|	Ashley	|63|	B|

3. SELECT clause execution
   
Select section_,sum(marks) query will only decide which columns to prints . It is decided to print section_ and sum(marks) column .

|section_	|sum|
|-----|----|
|D|	185|
|A|	245|
|B|	131|

4. ORDER BY clause execution
   
Order by section_ query will sort the rows ascending order.

|section_|	sum|
|-----|----|
|A	|245|
|B|	131|
|D|	185|

5. LIMIT clause execution
   
LIMIT 2; will only print first 2 rows.

|section_	|sum|
|-----|----|
|A	|245|
|B	|131|

This is how we got our final output.

