# Wild Cards

Grab a data that matches a specific pattern

% = any # characters,
_ = one character

```SQL
SELECT * FROM client WHERE client_name LIKE '%LLC' #any character before LLC 

SELECT * FROM client WHERE client_name LIKE '____-10%' 
#shows ppl born in october
```

# UNION

 Combine SELECT statements 
 
 You can do multiple unions
 
 Should have:
 * Same no. of Columns
 * Same DataType
 
 
 ```SQL
 SELECT first_name
 FROM employee;
 UNION
 SELECT branch_name
 FROM branch;
 #return first name and branch name in a single columm
 ```

# Joins

Combines *Rows* From 2 or more Tables

```SQL
SELECT employee.emp_id, employee.first_name, branch.branch_name
FROM employee
JOIN branch   
ON employee.emp_id = branch.mgr_id; 
# get employee.emp_id and branch.mgr_id and then display those emp_id which match
# Then also display branch name  in a single Table

#When using LEFT JOIN all employee from FROM employee gets displyed
#When using RIGHT JOINT it displays all Branch Table data

```
