# Functions Used in SQL 

![image](https://user-images.githubusercontent.com/102249128/201331265-83b7519b-940f-4d09-b60d-ec5ac60e5147.png)


```SQL
SELECT COUNT(emp_id)
FROM employee;    # count no. of employees 

SELECT COUNT(emp_id)
FROM employee  
WHERE sex='F' AND birth_date > '1971-01-01' ;
#Female employess who are born after 1970

SELECT AVG(salary)
FROM employee   #average salary

SELECT COUNT(emp_id)
FROM employee  
WHERE sex='M';  #Avg salarry of male

SELECT SUM(salary)
FROM employee   # total salary comapny is paying 

SELECT COUNT(sex), sex
FROM employee  
GROUP BY sex;  # tells us how many females and males (aggrigation)

SUM(total_sales),client_id
FROM works_with
GROUP BY client_id; #gives amount each client has spent

```
