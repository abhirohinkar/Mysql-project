# Mysql-project
sql employee project
SELECT * FROM org.worker;
INSERT INTO Worker 
	(WORKER_ID, FIRST_NAME, LAST_NAME, SALARY, JOINING_DATE, DEPARTMENT) VALUES
		(001, 'Monika', 'Arora', 100000, '14-02-20 09.00.00', 'HR'),
		(002, 'Niharika', 'Verma', 80000, '14-06-11 09.00.00', 'Admin'),
		(003, 'Vishal', 'Singhal', 300000, '14-02-20 09.00.00', 'HR'),
		(004, 'Amitabh', 'Singh', 500000, '14-02-20 09.00.00', 'Admin'),
		(005, 'Vivek', 'Bhati', 500000, '14-06-11 09.00.00', 'Admin'),
		(006, 'Vipul', 'Diwan', 200000, '14-06-11 09.00.00', 'Account'),
		(007, 'Satish', 'Kumar', 75000, '14-01-20 09.00.00', 'Account'),
		(008, 'Geetika', 'Chauhan', 90000, '14-04-11 09.00.00', 'Admin');
        
        CREATE TABLE Bonus (
	WORKER_REF_ID INT,
	BONUS_AMOUNT INT(10),
	BONUS_DATE DATETIME,
	FOREIGN KEY (WORKER_REF_ID)
		REFERENCES Worker(WORKER_ID)
        ON DELETE CASCADE
);
SELECT * FROM Bonus;
INSERT INTO Bonus 
	(WORKER_REF_ID, BONUS_AMOUNT, BONUS_DATE) VALUES
		(001, 5000, '16-02-20'),
		(002, 3000, '16-06-11'),
		(003, 4000, '16-02-20'),
		(001, 4500, '16-02-20'),
		(002, 3500, '16-06-11');
        
        UPDATE org.Bonus
SET  WORKER_REF_ID = 004 
WHERE BONUS_AMOUNT = 4500 and WORKER_REF_ID = 001;

        UPDATE org.Bonus
SET  WORKER_REF_ID = 005
WHERE BONUS_AMOUNT = 3500 and WORKER_REF_ID = 002;

        CREATE TABLE Title (
	WORKER_REF_ID INT,
	WORKER_TITLE CHAR(25),
	AFFECTED_FROM DATETIME,
	FOREIGN KEY (WORKER_REF_ID)
		REFERENCES Worker(WORKER_ID)
        ON DELETE CASCADE
);

INSERT INTO Title 
	(WORKER_REF_ID, WORKER_TITLE, AFFECTED_FROM) VALUES
 (001, 'Manager', '2016-02-20 00:00:00'),
 (002, 'Executive', '2016-06-11 00:00:00'),
 (008, 'Executive', '2016-06-11 00:00:00'),
 (005, 'Manager', '2016-06-11 00:00:00'),
 (004, 'Asst. Manager', '2016-06-11 00:00:00'),
 (007, 'Executive', '2016-06-11 00:00:00'),
 (006, 'Lead', '2016-06-11 00:00:00'),
 (003, 'Lead', '2016-06-11 00:00:00');
 
 SELECT * FROM org.worker;
 SELECT * FROM org.Bonus;
 SELECT * FROM org.Title;
 
 #2nd highest or 2,3,4th salaries.
 select * from org.worker where SALARY <> (select max(SALARY) from org.worker) 
 group by SALARY 
 ORDER BY SALARY desc
 limit 3;
  select FIRST_NAME, max(SALARY) from org.worker where SALARY <> (select max(SALARY) from org.worker);
  
 #Write an SQL query to fetch “FIRST_NAME” from Worker table using the alias name as <WORKER_NAME>.
 Select FIRST_NAME AS WORKER_NAME from org.Worker;
 
 #Write an SQL query to fetch unique values of DEPARTMENT from Worker table.<WORKER_NAME>.
 Select distinct DEPARTMENT from org.Worker;

#Write an SQL query to print the FIRST_NAME and LAST_NAME from Worker table into a single column COMPLETE_NAME. A space char should separate them.
Select CONCAT(FIRST_NAME, ' ', LAST_NAME) AS 'COMPLETE_NAME' from org.Worker;

#Write an SQL query to print all Worker details from the Worker table order by FIRST_NAME Ascending.
Select * from org.Worker order by FIRST_NAME asc;

#Write an SQL query to print details for Workers with the first name (in/(not in)) as “Vipul” and “Satish” from Worker table
Select * from org.Worker where FIRST_NAME in ('Vipul','Satish');
Select * from org.Worker where FIRST_NAME not in ('Vipul','Satish');

#Write an SQL query to print details of Workers with DEPARTMENT name as “Admin”.
Select * from org.Worker where DEPARTMENT like 'Admin%';

#Write an SQL query to print details of the Workers whose FIRST_NAME ends with ‘a’.
Select * from org.Worker where FIRST_NAME like '%a';

#Write an SQL query to print details of the Workers whose SALARY lies between 100000 and 500000.
Select * from org.Worker where SALARY between 100000 and 500000;

#Write an SQL query to print details of the Workers who have joined in Feb’2014.
Select * from org.Worker where year(JOINING_DATE) = 2014 and month(JOINING_DATE) = 2;

#Write an SQL query to fetch the count of employees working in the department ‘Admin’.
SELECT COUNT(*) FROM org.worker WHERE DEPARTMENT = 'Admin';

#Write an SQL query to fetch worker names with salaries >= 50000 and <= 100000.
SELECT CONCAT(FIRST_NAME, ' ', LAST_NAME) As Worker_Name, Salary
FROM org.worker 
WHERE Salary BETWEEN 50000 AND 100000;

#Write an SQL query to fetch the no. of workers for each department in the descending order.
SELECT DEPARTMENT, count(WORKER_ID) No_Of_Workers 
FROM org.worker 
GROUP BY DEPARTMENT 
ORDER BY No_Of_Workers DESC;
# Write an SQL query to show odd/even rows from a table.
SELECT * FROM org.Worker WHERE MOD (WORKER_ID, 2) <> 0;
SELECT * FROM org.Worker WHERE MOD (WORKER_ID, 2) = 0;
#Write an SQL query to clone a new table from another table.
CREATE TABLE WorkerClone LIKE org.Worker;
SELECT * FROM WorkerClone
#Write an SQL query to show the top n (say 10) records of a table.
SELECT * FROM org.Worker ORDER BY Salary desc LIMIT 10;
#Write an SQL query to fetch the list of employees with the same salary.
Select distinct W.WORKER_ID, W.FIRST_NAME, W.Salary 
from org.Worker W, org.Worker W1 
where W.Salary = W1.Salary 
and W.WORKER_ID != W1.WORKER_ID;

#Write an SQL query to fetch the first 50% records from a table.
SELECT *
FROM org.worker
WHERE WORKER_ID <= (SELECT count(WORKER_ID)/2 from org.Worker);

#Write an SQL query to fetch the departments that have less than five people in it.
SELECT DEPARTMENT, COUNT(WORKER_ID) as 'Number of Workers' FROM org.Worker 
GROUP BY DEPARTMENT 
HAVING COUNT(WORKER_ID) < 5;

# or 
select DEPARTMENT, count(WORKER_ID) from org.worker where DEPARTMENT < 5
group by department;

#Write an SQL query to show all departments along with the number of people in there.
SELECT DEPARTMENT, COUNT(DEPARTMENT) as 'Number of Workers' FROM 
org.Worker GROUP BY DEPARTMENT;

# Write an SQL query to fetch the names of workers who earn the highest salary.
SELECT FIRST_NAME, SALARY from org.Worker WHERE SALARY=(SELECT max(SALARY) from org.Worker);

#Write an SQL query to show the last/first record from a table.
 Select * from org.Worker where WORKER_ID = (SELECT max(WORKER_ID) from org.Worker);
 Select * from org.Worker where WORKER_ID = (SELECT min(WORKER_ID) from org.Worker);
  
 select WORKER_REF_ID, WORKER_ID, BONUS_AMOUNT, BONUS_DATE, FIRST_NAME, LAST_NAME from org.Bonus b 
 right join org.worker w on b.WORKER_REF_ID = w.WORKER_ID;
 
  select WORKER_REF_ID, WORKER_ID,  FIRST_NAME, LAST_NAME, BONUS_AMOUNT, BONUS_DATE from org.Bonus b 
 left join org.worker w on b.WORKER_REF_ID = w.WORKER_ID;
 
   select WORKER_REF_ID, WORKER_ID,  FIRST_NAME, LAST_NAME, BONUS_AMOUNT, BONUS_DATE from org.Bonus b 
 right join org.worker w on b.WORKER_REF_ID = w.WORKER_ID 
 where BONUS_AMOUNT <> (select max(BONUS_AMOUNT) FROM org.Bonus)
 order by BONUS_AMOUNT DESC;
 
  select WORKER_REF_ID, WORKER_ID,  FIRST_NAME, LAST_NAME, BONUS_AMOUNT, BONUS_DATE from org.Bonus b 
 right join org.worker w on b.WORKER_REF_ID = w.WORKER_ID
 where FIRST_NAME like '%ka%' ;
 
 select avg(SALARY), department FROM org.worker 
 group by department;
 
 
