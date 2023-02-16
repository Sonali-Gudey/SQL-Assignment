# Sql_PeerReview


### Arin's Approach:
##### Question-1:

```
SELECT Department, 
SUM(CASE
		WHEN Gender='Male' THEN 1 
        ELSE 0 END
	) as 'Num of males',
SUM(CASE
		WHEN Gender='Female' THEN 1 
        ELSE 0 END
	) as 'Num of females' 
FROM employees 
GROUP BY Department
ORDER BY Department;
```

- First Arin created a database using CREATE statement, he then created a table named 'employee' within the database which contains columns EmpID, Name, Gender, Department.
- His query selects the 'Department' column and uses two aggregate functions SUM along with two CASE statements to count the number of male and female employees in each department.
- In the first SUM function, the CASE statement he used will return 1 if the condition is true, else it retirns 0. The SUM function then adds up the values of each department which gives us the number of male employees in that daepartment.
- Similarly in the second SUM function it uses CASE and returns the number of females in each department.
- Now the GROUP BY clause groups the data by department, so that the results are shown for each department seperately.
- ORDER BY clause sorts the results by department name in ascending order.


##### Question-2:

```
SELECT Name, 
(SELECT MAX(maxSal) maxSal FROM 
	(SELECT salaries.Jan AS maxSal 
		UNION 
        SELECT salaries.Feb 
        UNION 
        SELECT salaries.Mar
	) AS a
) as Value,
(SELECT(
		CASE 
			WHEN Value=salaries.Jan THEN 'Jan' 
			WHEN Value=salaries.Feb THEN 'Feb' 
			WHEN Value=salaries.Mar THEN 'Mar' 
			END
		)
) as Month
FROM salaries;
```

- SELECT statement in Arin's query selects 'Name' column from 'salaries' table and two subqueries which calculate maximum salary value and the month in which it is earned.
- The first subquery uses MAX() function to determine the maximum value from a temporary table created by the UNION operator. This UNION operator is used to combine the salaries in all the months into a single column called 'maxSal'.
- The second subquery uses a CASE statement to determine the month in which the maximum salary value was earned.
- The query uses two subqueries to calculate the maximum salary value and the month in which it was earned, and then uses a CASE statement to determine the month name for the corresponding maximum value.


##### Question-3:

```
SET @rank_num=0;
SELECT 
	Marks, 
	@rank_num := @rank_num+1 as 'Rank', 
	GROUP_CONCAT(Candidate_ID) as Candidate_ID 
FROM marks 
GROUP BY Marks 
ORDER BY Marks DESC;
```

- In this query Arin used 'rank_num' variable that keeps track of the current rank.
- The rank_num column, increments the rank number by 1 for each row and the GROUP_CONCAT(Candidate_ID) which concatenates values for each group of marks.
- The GROUP BY clause groups the data by marks. This means that all rows with the same value of Marks will be grouped together.
- The ORDER BY clause sorts the data by marks in descending order, in which we get the rows with the highest marks first.


##### Question-4:

```
SELECT MIN(Candidate_id) as Candidate_id, Email FROM emails GROUP BY Email ORDER BY Candidate_id DESC;  
```

- The query selects two columns MIN(Candidate_id), which returns minimum Candidate_id value of each group of emails and 'Email'.
- The GROUP BY, groups the data by Email. This means that all rows with the same email address will be grouped together.
- The ORDER BY clause sorts the data by Candidate_id in descending order. 


### Ankit's Approach:
##### Question-1:

```
SELECT Department, 
SUM(CASE
		WHEN Gender='Male' THEN 1 
        ELSE 0 END
	) as 'Num of males',
SUM(CASE
		WHEN Gender='Female' THEN 1 
        ELSE 0 END
	) as 'Num of females' 
FROM employees 
GROUP BY Department
ORDER BY Department;
```

 - In Ankit's query, the first SUM function uses a conditional statement to count the number of male employees in each department. It checks if the "gender" column is "Male" and returns a 1 if true, and a 0 if false. The SUM function is then used to add up all the 1's to get the total number of male employees. This is aliased as "Count of Male".
 - The second SUM function works the same way as the previous one, but counts the number of female employees instead. It checks if the "gender" column is "Female" and returns a 1 if true, and a 0 if false. The SUM function is then used to add up all the 1's to get the total number of female employees. This is aliased as "Count of Female".
 - Finally, the query groups the results by department using the "GROUP BY" clause. This gives the total number of male and female employees in each department.


##### Question-2:

```
SELECT Name,
       CASE
           WHEN Jan>=Feb AND Jan>=Mar THEN Jan
           WHEN Feb>=Jan AND Feb>=Jan THEN Feb
           ELSE Mar
       END AS Value,
       CASE
           WHEN Jan>=Feb AND Jan>=Mar THEN 'Jan'
           WHEN Feb>=Jan AND Feb>=Jan THEN 'Feb'
           ELSE 'Mar'
       END AS Month
 FROM employee_info; 
```
- The query calculates the highest value among the three columns (Jan, Feb, and Mar) using a "CASE" statement. If the value in January is greater than or equal to February and March, then it selects January as the highest value.Similarly for the remaining as well.
- The query also determines which month has the highest value for each employee using another "CASE" statement. If January has the highest value, then it selects 'Jan' as the corresponding month. If February has the highest value, then it selects 'Feb'. Otherwise, it selects 'Mar'.



##### Question-3:

```
SELECT Marks, 
       RANK() OVER(ORDER BY Marks DESC) 'Rank',
       GROUP_CONCAT(CandidateID) AS CandidateID
FROM EXAM
GROUP BY Marks
ORDER BY Marks DESC;
```

- The query uses the RANK() function to assign a rank to each row based on the marks in descending order. The GROUP_CONCAT() function is used to concatenate the candidate IDs for each group of marks, and the GROUP BY clause is used to group the results by marks.
- The result set will be ordered by the marks in descending order.

##### Question-4:

```
create view Help_info as SELECT MIN(CandidateId) AS Candidate_ID
FROM Records
GROUP BY Email
ORDER BY Candidate_ID DESC ;
select * from Help_info;
--deleting
DELETE from records where candidateId not in
(select candidate_Id from Help_info); 
```

- The first part of the SQL query creates a view called "Help_info" that selects the minimum CandidateId for each unique Email in the Records table, and then orders the results in descending order by the Candidate_ID.
- The second part of the SQL query is a DELETE statement that removes all records from the Records table where the CandidateId is not present in the Help_info view.
- This effectively deletes all but the oldest record for each unique email address in the Records table, as determined by the minimum CandidateId.
