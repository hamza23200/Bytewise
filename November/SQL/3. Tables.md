# Data Types 
![image](https://user-images.githubusercontent.com/102249128/201202122-7cdb43a8-a2c3-4f39-a19b-c9f71962b4c3.png)

Decimal(M,N) 

M = no. of digits to store (total)
N = no. of digits after Decimal

VARCHAR(100) = string length 100

BLOB = stores images and files

*USE SQL RELATED COMMANDS IN CAPS ON TO DISTINGUISH EASILTY*
*END ALL STATMENTS WITH ;*
*ON POPSQL YOU CAN RUN CODE LINE BY LINE JUST LIKE IN JUPYTER NOTEBOOK*
*NOT EQUAL TO COMMAND  <>*

# Create Tables 
To create:
![image](https://user-images.githubusercontent.com/102249128/201203265-8c449cdd-4d96-4a49-983a-972e307dd7d9.png)


```SQL
create database sql_workbench;
use sql_workbench;

CREATE TABLE student(
student_id INT PRIMARY KEY,
name VARCHAR(20) NOT NULL,
major VARCHAR(20) 
); #Database Schema

#CONSTRAINTS:

#NOT NULL  #shouldnt be empty 
#UNIQUE   #should be uniqiue 
#DEFAULT 'undecided' #puts unchanged if no major given
#student_id INT AUTO_INCREMANT #data automatically gets incremented when inserted


# DESCRIBE student # describes the table and shows info
# DROP TABLE #deletes the table 
# ALTER TABLE student ADD gpa DECIMAL(3,2) #adds extra column 
# ALTER TABLE student DROP COLUMN gpa #delets gpa column
# SELECT * FROM student  #shows all info

INSERT INTO student VALUES(1,'Jack','Biology'); 
# CHANGE INFO TO ADD NEW INFO LIKE 2,KATE,SOCIO
# Another way to do this INSERT INTO student(student_id,name) VALUES(3,'Claire');

INSERT INTO student VALUES(2,'kate','Sociology'); 
INSERT INTO student(student_id,name) VALUES(3,'Claire')
INSERT INTO student VALUES(4,'Jack','Biology'); 
INSERT INTO student VALUES(5,'Mike','Computer Science'); 

UPDATE student #update tables
SET major = 'Bio';
WHERE major = ' Biology '; # you can change these conditions

DELETE FROM student #delets row
where student_id=5;

 
# SELECT means what information you want and FROM where(Table) 
# ORDER BY name DESC #order the tables in alphabetical order(Z->A) or ASC (A->Z)
# LIMIT 2 # Gives only 2 results
# WHERE major='Biology' OR major= 'Chemistry' #gives bio & chem major ppl 
# WHERE name IN ('Claire','Kate','Mike')






```
