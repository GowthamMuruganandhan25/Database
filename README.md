Data is stored in typical Relational Database

Database-->collection of tables
Table-->contains actual data

sql-->Structured Query Language   
-->All statements in the sql ends with the semi-colon;
-->It is a case-insensitive 
-->But the date inside the cells is case-sensitive in the database

Table contains Rows/data/record and columns
columns contain information of same type

Data science is all about analysis and extracting the data.

constraint:

Database ability to control what kind of data should be go through the column..

PRIMARY KEY
-->It is a constraint
-->It prevent duplicate information from being inserted in the given column
-->unique data inserted in the given column
-->It allows null values 
-->only one primary key should be in the table

create table departments(
department varchar(20),
division varchar(20),
primary key (department));

insert into departments values('automotive','auto');
insert into departments values(' ','domestic');
insert into departments values('clothing','domestic');
insert into departments values('a','');
insert into departments values(' ',' ');  ORA-00001: unique constraint
insert into departments values('NOT NULL','a');  ORA-00001: unique constraint

create table regions(
region_id int,
region varchar(20),
country varchar(20)
);

insert into regions values(1,'a',' ');
insert into regions values('','b','c');
insert into regions values(' ','','');  --->for number we should not have to keep space   -->ORA-01722
insert into regions values('',' ',' '); or
insert into regions values('','','');


Select statement--->is a particular kind of statement often referred to as "Query" 
why they call as query?
It is basically  a question that you ask database.The information retrieve from the database what are you looking for

-->It is all about getting information(answer) from the answer..

Where Clause
-->Basically filters specific records

select * from employees where department = 'Furniture';

select * from employees where department like '%nitu%'; --->like     if the starting character is not known-->'%urnirure'
select * from employees where department like '%nitu                 if the ending character are known-->'Fu%'

Filter using numeric  using <,>,=,<> or != -->not equal to or <! or >!

select * from employees where salary > 10000;
select * from employees where salary = 61256;

condition that evaulates true or false

select * from employees where 1=1;

select * from employees where 1 < 1;--->query will be executed and return nothing

Multiple conditions:

select * from employees where department = 'Clothing' AND salary > 90000;

select * from employees where department = 'Clothing' AND salary > 20000 AND region_id  > 4;

AND Clause --->AND clause must be true for all the conditions   //It will executed but does not return any information in the database

OR OPERATOR-->It's not compulsory for the condition to be true

select * from employees where department = 'Clothing' OR salary > 2000; 

select * from employees where salary < 40000 or department='Clothing' or department='Pharmacy'; // works but not gives all records


select * from employees where salary > 40000 AND (department='Clothing' or department like'%urniture');

()-->Presents of paranthesis causes the condition within them to be evaulated together..

select * from employees where department = 'Sports' AND department = 'Tools'; --> logically inaccurate.


USING FILTERING OPERATORS-->IN,NOT IN,IS NULL,BETWEEN

NOT-->condition is opposite if it is true it will be false and vice-versa

select * from employees where NOT department = 'Sports';  // gives records other than "sports"

select * from employees where NOT department <> 'Sports'; // It will execute but gives same department

select * from employees where department != 'Sports';

NO means--->Empty data

select * from employees where null != null;  // It will executed but does not return any information in the database

select * from employees where  email is null;  //given null values in the record

select * from employees where  email is not null; //gives values in the record


IN--->select * from employees where department in ('Sports','First Aid');


BETWEEN-->select * from employees where department between 80000 and 10000;

sql comments --

Assignments::
select first_name,hire_date from employees where salary > 165000 or (department='sports' and gender='m');
select * from employees where salary>40000 and salary<10000 and department='automotive' and gender='m' or(gender='f' and department='toys');
select first_name,email from employees where gender='F' and department='tools' and salary > 110000;

ORDER BY:--->sorting

-->should be last in the statement

ASCENDING AND DESCENDING

-->by default it is ascending

select * from employees order by department;
select * from employees order by department desc;

DISTINCT-->gives unique values

select distinct department from employees order by department desc;
(or)
select distinct department from employees order by 1 asc;

LIMIT
select distinct department from employees order by department limit 10;

FETCH-->ie fetch first 10 rows only

select distinct department from employees order by department fetch first 3 rows only;

AS-->change the column names or rename the columns

upper(),lower(),,length(),trim(),+boolean expression and concatenation

UPPER AND LOWER::
select upper(first_name),lower(last_name) from employees;

length()::
select length(first_name),lower(last_name) from employees;

Trim()-->used to remove whitespace 

select length(trim(first_name)) from employees;

||-->concatenation of two columns into single columns

select first_name ||' '||last_name from employees;

select first_name ||' '||last_name full_name from employees; --->column name is full name we don;t need to use as


Boolean expression


select first_name ||last_name full_name,(salary > 50000) from employees;-->shows true or false

select department, (department like '%oth%') from employees;


STRING FUNCTIONS SUBSTRING(),REPLACE(),POSITION() AND COALESCE()

SUBSTRING()::

select substring('this is data' from 1 to 4) test_data_extracted  select substring('this is data' from 3) test_data_extracted

output:this,is is test data

Replace()::

select department,replace(department,'Clothing','Attire') modified_data from employees;

assignment-->select department,replace(department,'Clothing','Attire') modified_data,department ||'department' combined_dept from employees;

Position()::position of a particular character

select position('@' in email ) from employees;

select substring(email,position('@' in email) from employees; o/p-->@abc.net.au

select substring(email,position('@' in email + 1) from employees; o/p-->abc.net.au


coalesce():: in the empty cell it will set something

select coalesce(email,'no') as email from employees;



Grouping functions min(),max(),avg(),sum(),count()

select count(email) from employee;

select count(*) from employees;

select sum(salary) from employees;



Grouping--->Any non agreegate column mentioned in the select should also be mentioned in the group by clause


create table cars(
make varchar(10));

select * from cars;

insert into cars values('Honda');
insert into cars values('Honda');
insert into cars values('Honda');
insert into cars values('Toyota');
insert into cars values('Toyota');
insert into cars values('Nissan');


select count(*) from cars group by make;

select make,count(*) from cars group by make;

Group By and Having clause::

Group by-->It goes after the where clause

select department,sum(salary) from employees where 1=1 group by department;

select department,sum(salary) from employees where region_id in(4,5,2,6) group by department;

select department,count(*) from employees group by department;


select department,count(*),avg(salary),min(salary),max(salary) from employees group by department;

select department,count(*),round(avg(salary)),min(salary),max(salary) from employees group by department order by department desc;

select department,region_id,count(*) from employees group by department,region_id order by department desc;


Having-->to filter the  aggregate data we use the having clause

Having comes after group by clause..before order by

select department,count(*) from employees group by department having count(*) < 3 order by department;

Assignments:
select  substring(email,position('@' in email) +1),count(*) from employees where email is not null group by substring(email,position('@' in email) +1);

select gender,region_id,min(salary),max(salary),round(avg(salary)) from employees group by region_id,gender order by gender;

select gender,region_id,min(salary),max(salary),round(avg(salary)) from employees group by region_id,gender order by region_id;


Aliasing sources of data:

you can refer the columns of specific tables by specifiying the table name before the particular column

select employees.department from employees,departments;

select e.department from employees e,departments d


Sub queries -->query inside the query is called sub-query

select * from employees where department not  in(select department from departments);

select e.first_name,e.email from (select * from employees where salary > 140000) e -->using alias name

select e.first_name.e.email from(select first_name employee_name, email mail_id from employees) e---> ORA-00904: "E"."FIRST_NAME"."E"."EMAIL": invalid identifier


Assignments::

-->select * from employees where salary > 130000 and region_id in (select region_id from regions where country='Asia' or country='Canada');

-->select first_name,department,(select max(salary) from employees)-salary from employees where region_id in (select region_id from regions where country='Asia' or country='Canada')

select * from employees where region_id in(select region_id from regions where country ='United States')


ALL/ANY CLAUSE-->used in group by and having by clause

select * from employees where region_id > all (select region_id from regions where country ='United States')

CASE STATEMENT-->conditional expression

select first_name, salary,
case
when salary<100000 then 'under paid'
when salary>100000 then 'paid well'
end
from employees

select first_name, salary,
case
when salary<100000 then 'under paid'
when salary>100000 then 'paid well'
else 'unpaid'
end
from employees order by salary desc;


select a.category,count(*) from(
select first_name, salary,
case
when salary<100000 then 'under paid'
when salary>100000 and salary < 1600000 then 'paid well'
else 'executive'
end as category
from employees order by salary desc) a group by a.category;



select sum(case when salary < 100000 then 1 else 0 end ) as under_paid,              
sum(case when salary < 100000 then 1 else 0 end ) as paid_well,
sum(case when salary < 150000 then 1 else 0 end ) as executive
from employees;

o/p--->
UNDER_PAID	PAID_WELL	EXECUTIVE
12	12	18

TRANSPOSING DATA:

select sum(case when department='Sports' then 1 else 0 end) as Sports,
sum(case when department='Tools' then 1 else 0 end) as Tools,
sum(case when department='Clothing' then 1 else 0 end) as Clothing,
sum(case when department='Computers' then 1 else 0 end) as Computers
from employees;



select first_name,
when region_id=1 then (select country from regions where region_id=1) end region_1  from employees;
when region_id=2 then (select country from regions where region_id=2) end region_2
from employees


windowing functions: over() is the windowing functions

select first_name,department,count(*) over(partition by department) from employees;

select  first_name,department,
count(*) over(partition by department), 
count(*) over(partition by region_id) from employees;

select first_name,department,count(*) over() from employees where region_id=3;

ORDERING DATA IN WINDOW FRAMES


select first_name,hire_date,salary,sum(salary) over (order by hire_date range between unbounded preceding and current row) from employees;

select first_name,hire_date,salary,department,sum(salary) over (partition by department order by hire_date) from employees;

select first_name,hire_date,department,salary,sum(salary) over(order by hire_date rows between 3 preceding and current row) from employees;

RANKING AND BUCKETING

select first_name,email,department,salary,rank() over(partition by department order by salary desc) from employees;

select first_name,email,department,salary,first_value(salary) over(partition by department order by salary desc) first_value from employees;



First_value function()

select first_name,email,department,salary,first_value(salary) over(partition by department order by salary desc) first_value from employees;



LEAD AND LAG FUNCTIONS::


lead--->shows the next column data example-->shows the salary of the next person in the same column

lag--->shows the previous column data


Working with Rollups and Cubes

GROUPING SETS::


select continent,country,city,sum(units_sold)
from sales
group by grouping sets(continent,country,city)

select continent,country,city,sum(units_sold)
from sales
group by ROLLUP(continent,country,city)

CUBE-->


select continent,country,city,sum(units_sold)
from sales
group by CUBE(continent,country,city)



JOINS -->links the data from two tables with the same column

select first_name,country from employees,regions where regions.region_id=employees.region_id

select first_name,email,division from employees,departments where employees.department = departments.department

select first_name,email,division,country from employees,departments,regions where employees.department = departments.department
and employees.region_id=regions.region_id
and email is not null

select country,count(employee_id) from employees,regions where employees.region_id=regions.region_id group by country;


INNER JOINS--->only matching data it will display

select first_name,email,division from departments inner join employees on departments.department=employees.department  inner join regions on
employees.region_id = regions.region_id------------>joining 2 tables

select first_name,email,division,country from departments inner join employees on departments.department=employees.department  inner join regions on
employees.region_id = regions.region_id ----------->joining 3 tables


OUTER JOINS  1..LEFT OUTER JOIN---->not matching values will also be displayed only left value table will be given(remaining data of left table will be given)
             2..RIGHT OUTER JOIN--->not matching values will also be displayed only right value table will be given(remaining data of right table will be given)
			 3..FULL OUTER JOIN--->displays matching and non matching values in both the tables
			 
1-->select distinct employees.department,departments.department from employees left outer join departments on employees.department=departments.department

2-->select distinct employees.department,departments.department from employees right outer join departments on employees.department=departments.department

3-->select employees.department,departments.department from employees full outer join departments on employees.department=departments.department

NOTE-->To use union no of columns should match and datatype should also match

UNION-->it removes duplicates 

select  department from employees union select  department from departments


UNION ALL-->it does not remove duplicates


select  department from employees
union all
select  department from departments


EXCEPT-->select distinct department from employees EXCEPT select distinct department from departments;


CARTESIAN PRODUCT-->occurs when there is no joins


CORRELATED SUBQUERIES:--->very slow
-->It runs for every single records

-->A query nested inside the other that uses the values from outer query (or) The inner query obtained the information from the other query


select first_name,salary from employees e1 where salary > (select round(avg(salary)) from employees e2 where e1.department = e2.department)

select first_name,department,salary,(select round(avg(salary)) from employees e2 where e1.department = e2.department) as avg_department from employees e1

-------------------------------------------------------------------------------------------------------------------------------------

