# Pewlett-Hackard-Analysis

## Project Overview 
### Purpose
The purpose of this analysis is to prepare Pewlett-Hackard, a company with several thousand employees, for the upcoming “silver tsunami”. A large number of employees will begin retiring at a rapid rate in the next few years and the company wants to be prepared with the retirement packages, open positions and employees’ training. In order to ensure a smooth transition this analysis focuses on the following: 

1.	Identify the retiring employees by their title.
2.	Determine the sum of retiring employees grouped by title.
3.	Identify the employees eligible for participation in the mentorship program.
4.	Determine the number of roles-to-fill grouped by title and department.
5.	Determine the number of qualified, retirement-ready employees to mentor the next generation grouped by title and department.

## Results  

**1.	The list of retiring employees**
-	The table includes employee number, first name, last name, title, from-date and to-date.
-	The table displays a list of employees who is going to retire in the next few years.
-	The list is long and extensive, yet at-a-glance analysis gives us some insights about the query. Some employees appear more than once due to change of title during their career at Pewlett-Hackard. It happened because it contained all the titles that employees acquired while working at Pewlett-Hackard over the years. This resulted in duplicates, some employees appear two times or more; therefore, the number of retiring employees was  incorrect
-	
<p align="center">  
<img src="" width="50%" height="50%">
</p>
<p align="center">  
<i>Figure : Table with the employee’s data that are retirement-ready</i>
</p>

  **Overview of the code**
  
To retrieve the data, two tables were merged together - employees and titles - with the `inner join` and filtered by birth date, that indicates who is about to retire in the next few years with the command `WHERE (e.birth_date BETWEEN '1952-01-01' AND '1955-12-31')`. 


**2.	The list of retiring employees without duplicates**
-	The table includes employee number, first name, last name, title, from-date and to-date. 
- The table displays a list of employees who are going to retire in the next few years.
-	In the table each employee is listed only once, by her or his most recent title.
-	
<p align="center">  
<img src="" width="50%" height="50%">
</p>
<p align="center">  
<i>Figure : Table with the employee’s data that are retirement-ready without duplicates</i>
</p>

**Overview of the code**

Query contains the same data as the query above with addition of `distinct_on` command that kept only unique values. To ensure that most recent values are kept, I used command `ORDER BY rt.emp_no, rt.to_date DESC` to sort the data by descending order on the `to_date` column. In this case the most recent title was listed first, and after running the query the duplicates listed after the first appearance of the same employees were removed.

**3.	The number of retiring employees grouped by title**
-	The table includes employees’ titles and their sum. 
-	The query returns a cohesive table with 7 rows.
-	From this table we can quickly see how many employees with certain title will retire in the next few years.

<p align="center">  
<img src="" width="30%" height="30%">
</p>
<p align="center">  
<i>Figure : Table with the employee grouped by title</i>
</p>

**Overview of the code**

In order to retrieve this table I used `GROUP BY ut.title` command, and it is responsible for grouping the rows by titles. Next, I used its corresponding command `COUNT (ut.title)` that counts how many times specific title appears in the database. 

**4.	The employees eligible for the mentorship program**
-	The table contains employee number, first name, last name, birth date, from date, to date and title. 
- The table displays a list of employees who is eligible for the mentorship program.
- 
<p align="center">  
<img src="" width="50%" height="50%">
</p>
<p align="center">  
<i>Figure : Table with the employee grouped by title</i>
</p>

**Overview of the code**

To retrieve this data, three tables were merge together: employees, titles and dep_emp with the `inner join`. The query filters by birth date (that indicates who is eligible for the mentorship program) with the command ` WHERE (e.birth_date BETWEEN '1952-01-01' AND '1955-12-31') ` and `to_date`  to include only current employees. Duplicates were removed by `DISTINCT ON (e.emp_no)` command. To ensure I got the most recent titles, I used `ORDER BY e.emp_no, ti.from_date DESC` command.


## Summary

As the company is preparing for the upcoming "silver tsunami" a good planning is essential, especially when such a large number of the employees is involved. Couple of key questions need to be answered.

***How many roles will need to be filled as the "silver tsunami" begins to make an impact?***<br>

The table **retirement titles** contains all the information about the employees that are about to retire in the next four years. To get the number of positions that will be open in next four years I ran additional query that breaks down how many staff will retire per department. Since every department will be affected in some way this query gives more precise numbers what each department can expect and how many roles will need to be filled.

<p align="center">  
<img src="Graphics/Extra_RolesToFill.PNG" width="40%" height="40%">
</p>
<p align="center">  
<i>Figure : Sum of retirement-ready employees group by title and department.</i> 
</p>



***Are there enough qualified, retirement-ready employees in the departments to mentor the next generation of Pewlett-Hackard employees?***<br>

To ensure that are enough qualified staff for training at Pewlett-Hackard I ran a query with additional filter, that returns only employees on higher positions, assuming that those are qualified as mentors. With the command ` WHERE ut.title IN ('Senior Engineer', 'Senior Staff', 'Technique Leader', 'Manager') ` the results include only staff on higher positions. From the table we can see that the mentorship pool is not evenly distributed, in some instances (sales manager and research manager) there is only one candidate. Which is not enough to mentor the next generation of Pewlett-Hackard employees . 

<p align="center">  
<img src="" width="40%" height="40%">
</p>
<p align="center">  
<i>Figure : Sum of qualified, retirement-ready employees group by title and department</i>
</p>




