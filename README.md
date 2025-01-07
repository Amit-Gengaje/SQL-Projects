1.	Input SQL Queries: 

CREATE DATABASE IF NOT EXISTS employee;
USE employee;
SET SQL_SAFE_UPDATES = 0;

Used the Table Data Import Wizard to import the three CEP dataset CSV files as tables “data_science_team”, “emp_record_table” and “proj_table”

2.	Input SQL Action: 

Database tab -> Reverse Engineer DB -> Select Schemas (Chose schema created above) -> kept clicking next

3.	Input SQL Query: 

SELECT emp_id, first_name, last_name, gender, dept FROM emp_record_table;

4.	Input SQL Query: 

SELECT emp_id, first_name, last_name, gender, dept, emp_rating FROM emp_record_table WHERE 
emp_rating <2
OR emp_rating >4
OR (emp_rating >=2 AND emp_rating <=4);

5.	Input SQL Query: 

SELECT CONCAT(first_name, '  ', last_name) NAME 
FROM emp_record_table WHERE dept = 'FINANCE';

6.	Input SQL Query: 

SELECT  manager_id, count(*)
FROM emp_record_table
GROUP BY manager_id
ORDER BY manager_id;

7.	Input SQL Query: 

Select first_name, last_name, dept FROM emp_record_table WHERE dept = 'HEALTHCARE' 
UNION 
SELECT first_name, last_name, dept FROM emp_record_table WHERE dept = 'FINANCE';

8.	Input SQL Query: 

SELECT emp_id, first_name, last_name, role, dept, emp_rating, max(emp_rating) 
Over (partition by dept) AS max_emp_rating
FROM emp_record_table;

9.	Input SQL Query: 

Select role, MIN(salary) AS min_salary,
MAX(salary) AS max_salary
FROM emp_record_table
GROUP BY ROLE;

10.	Input SQL Query: 

SELECT emp_id, first_name, last_name, exp, DENSE_RANK() OVER (ORDER BY EXP DESC) AS experience_rank 
FROM emp_record_table;
 
11.	Input SQL Query: 

CREATE VIEW employee_location AS
SELECT emp_id, first_name, last_name, country, salary FROM emp_record_table WHERE salary > 6000;

SELECT * FROM employee_location;
 
12.	Input SQL Query: 

SELECT * FROM emp_record_table WHERE emp_id
IN (SELECT emp_id FROM emp_record_table WHERE exp > 10);

13.	Input SQL Query: 

CREATE DEFINER=`root`@`localhost` PROCEDURE `exp_greater_than_three`()
BEGIN
select * from emp_record_table WHERE  exp > 3;
END

CALL employee.exp_greater_than_three();

14.	Input SQL Query: 

CREATE DEFINER=`root`@`localhost` PROCEDURE `job_profile`()
BEGIN
select * , case 
WHEN exp<=2 then 'JUNIOR DATA SCIENTIST'
WHEN exp>2 and exp<=5 then 'ASSOCIATE DATA SCIENTIST'
WHEN exp>5 and exp<=10 then 'SENIOR DATA SCIENTIST'
WHEN exp>10 and exp<=12 then 'LEAD DATA SCIENTIST'
WHEN exp>12 and exp<=16 then 'MANAGER'
end as job_prof_match FROM emp_record_table;
END

call employee.job_profile();

15.	Input SQL Query: 

SELECT * FROM emp_record_table ORDER BY first_name;
DESCRIBE emp_record_table; 
ALTER TABLE emp_record_table modify first_name VARCHAR(50);
CREATE INDEX fname_index ON emp_record_table(first_name);
SHOW INDEXES FROM emp_record_table;
SELECT * from emp_record_table WHERE first_name = "Eric";

16.	Input SQL Query: 

SELECT 
    EMP_ID,
    FIRST_NAME,
    LAST_NAME,
    SALARY,
    EMP_RATING,
    (0.05 * SALARY) * (EMP_RATING) AS BONUS
FROM
    emp_record_table;

17.	Input SQL Query: 

SELECT *  , avg(salary) over (partition by country) AS country_wise, 
avg(salary) over (partition by continent) AS continent_wise 
FROM emp_record_table;
