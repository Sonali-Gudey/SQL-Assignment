-- Creating a database.
CREATE DATABASE SQL_ASSIGNMENT;
USE SQL_ASSIGNMENT;


Question-1:


-- Creating a table employyes.
CREATE TABLE IF NOT EXISTS EMPLOYEES(
	EMP_ID INT NOT NULL UNIQUE,
	EMP_NAME VARCHAR(30),
	GENDER VARCHAR(10),
	DEPARTMENT VARCHAR(30),
	CHECK(GENDER IN ("Male","Female")));
    

-- Inserting values into employees table.
INSERT INTO EMPLOYEES VALUES 
	(1,'X','Female','Finance'),
    (2,'Y','Male','IT'),
    (3,'Z','Male','HR'),
    (4,'W','Female','IT');
	

-- Checking the condition given.
INSERT INTO EMPLOYEES VALUES(8,'W','Ab','IT');
INSERT INTO EMPLOYEES VALUES(11,'Y','Female',NULL);


-- Finding the number of male and female employees in each
department:
SELECT IFNULL(DEPARTMENT,'Dept not assigned') AS DEPARTMENT,
    COUNT(CASE WHEN UPPER(GENDER)='Male' THEN 1 END) AS 'No of male',
    COUNT(CASE WHEN UPPER(GENDER)='Female' THEN 1 END) AS 'No of Female'
FROM EMPLOYEES
GROUP BY DEPARTMENT
ORDER BY DEPARTMENT;




Question-2:




-- Creating table for employee salaries.
CREATE TABLE EMP_SALARIES (
	EMP_NAME VARCHAR(30) NOT NULL,
	Jan NUMERIC(15,2) NOT NULL DEFAULT 0,
	Feb NUMERIC(15,2) NOT NULL DEFAULT 0,
	Mar NUMERIC(15,2) NOT NULL DEFAULT 0,
	CHECK(Jan>=0 and Feb >=0 and Mar >=0));


 -- Inserting values into the table.     
INSERT INTO EMP_SALARIES VALUES
	('X',5200,9093,3832),
	('Y',9023,8942,4000),
    ('Z',9834,8197,9903),
    ('W',3244,4321,0293);


-- Checking the condition given.
INSERT INTO EMP_SALARIES VALUES('A',1996,-5078,NULL);
INSERT INTO EMP_SALARIES VALUES('B',2000,6762,NULL);


-- Find the max amount from the rows with month name:
SELECT EMP_NAME as NAME,
  VALUE,
  CASE WHEN idx=1 THEN 'Jan'
       WHEN idx=2 THEN 'Feb'
       WHEN idx=3 THEN 'Mar'
  END AS MONTH
FROM (
SELECT
  EMP_NAME,
  GREATEST(Jan, Feb, Mar) AS VALUE,
  FIELD(GREATEST(Jan, Feb, Mar), Jan, Feb, Mar) as idx
FROM
  EMP_SALARIES
) EMP;




Question-3:



-- Creating a table test.
CREATE TABLE TEST (
	CANDIDATE_ID INT NOT NULL UNIQUE,	
	MARKS FLOAT(10,2) DEFAULT 0);


-- Inserting values into the table test.
INSERT INTO TEST 
VALUES (1,98),
	  (2,78),
	  (3,87),
	  (4,98),
	  (5,78);


-- Ranking them in proper order by marks.
SELECT MARKS,DENSE_RANK() OVER (ORDER BY MARKS DESC ) AS 'RANK', GROUP_CONCAT(CANDIDATE_ID) AS CANDIDATE_ID
FROM TEST
GROUP BY MARKS;




Question-4:



-- Creating a table for email ids.
CREATE TABLE EMAIL_IDS (
	CANDIDATE_ID INT NOT NULL,
	EMAIL VARCHAR(30) NOT NULL);  

 
 -- Inserting records into the table.
INSERT INTO EMAIL_IDS 
VALUES (45,'abc@gmail.com'),
	  (23,'def@yahoo.com'),
	  (34,'abc@gmail.com'),
	  (21,'bcf@gmail.com'),
	  (94,'def@yahoo.com');


-- Finding duplicate mail ids in the table and if same value is repeated for different id, then keeping the value that has smallest id and deleting
all the other rows having same value:
DELETE FROM EMAIL_IDS 
WHERE CANDIDATE_ID IN (SELECT TEMPCANDIDATE_ID FROM (SELECT DISTINCT A.CANDIDATE_ID as TEMPCANDIDATE_ID 
FROM EMAIL_IDS AS A 
INNER JOIN EMAIL_IDS AS B
WHERE A.EMAIL=B.EMAIL AND A.CANDIDATE_ID>B.CANDIDATE_ID) AS C) 
ORDER BY CANDIDATE_ID;
