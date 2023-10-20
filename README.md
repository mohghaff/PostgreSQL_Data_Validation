Employee Dashboard Data Verification Documentation

Introduction
This documentation outlines the process of creating and verifying data from the Employee Dashboard in Power BI using a PostgreSQL database. To ensure data accuracy and integrity, a PostgreSQL database named "employee database" was established. Data was imported into a table, and various queries were executed to validate the dashboard's information.

Database Creation and Table Setup
PostgreSQL Database Creation
A PostgreSQL database named "employee database" was created to serve as the repository for the employee data used in the dashboard verification process.
Table Setup
A table named "employeedata" was created in the "employee database" to hold employee-related data. The table schema is as follows:
sql
Copy code
create table employeedata
(
	emp_no int8 PRIMARY KEY,
	gender varchar(50) NOT NULL,
	marital_status varchar(50),
	age_band varchar(50),
	age int8,
	department varchar(50),
	education varchar(50),
	education_field varchar(50),
	job_role varchar(50),
	business_travel varchar(50),
	employee_count int8,
	attrition varchar(50),
	attrition_label varchar(50),
	job_satisfaction int8,
	active_employee int8
)
Data Import
Data was imported into the "employeedata" table using the following query:
sql
Copy code
COPY employeedata FROM 'C:\Users\mghaf\OneDrive\Desktop\Data analysis\Employee Attrition Postgres' DELIMITER ',' CSV HEADER;
This query loaded the data from the specified CSV file into the table.

Data Verification Queries
1. Employee Count Verification
To verify the total number of employees in the database, the following query was executed:

sql
Copy code
select count(*) from employeedata;
2. Education Levels and Attrition Rate Verification
To verify the education levels of employees and their attrition rates, the following queries were executed:

Query to check education levels of employees and attrition rate:
sql
Copy code
select count(*) as attrition_count, education, attrition
from employeedata
group by education, attrition
order by education, attrition;
3. Attrition Rate by Gender Verification
To verify the attrition rate by gender, the following query was executed:

sql
Copy code
select count(*) as attrition_count, gender from employeedata
where attrition = 'Yes'
group by gender;
4. Attrition Count by Gender and Department Verification
To verify the attrition count by gender and department, the following query was executed:

sql
Copy code
select count(*) as attrition_count, gender, department from employeedata
where attrition = 'Yes'
group by gender, department
order by count(*);
5. Retention Count by Age and Department Verification
To verify the retention count by age and department, the following query was executed:

sql
Copy code
select count(*) as retention_count, age, department from employeedata
where attrition = 'No'
group by department, age
order by count(*) desc;
Conclusion
The PostgreSQL database and data verification queries were successfully employed to ensure the accuracy and integrity of data used in the Employee Dashboard in Power BI. This process confirms the reliability of the dashboard's information, allowing for informed decision-making and analysis based on verified data.