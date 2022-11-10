SQL is a language used for interacting with Relational Database Management Systems (RDBMS)

You can use SQL to get the RDBMS to do things for you
* Create, retrieve, update & delete data
* Create & manage databases
* Design & create database tables
* Perform administration tasks (security,
* user mana ement, im ort/ex ort, etc

SQL is actually a hybrid language, it's basically 4 types of languages in one

* Data Query Language (DQL)

    Used to query the database for information.

    Get information that is already stored there
    
* Data Definition Language (DDL)

    Used for defining database schemas.
    
* Data Control Language (DCL)

    Used for controlling access to the data in the database.

    User & permissions management
    
* Data Manipulation Language (DML)

    Used for insetting, updating and deleting data from the database
    
# Queries
A query is a set of instructions given to the RDBMS (written is
SQL) that tell the RDBMS what information you want it to
*retrieve* for you

```SQL
SELECT employee.name, employee.age
FROM employee
WHERE employee.salary>30000;
```

## MySOL Windows Installation

Google *mysql community server*

download and install,  
in installation :
![image](https://user-images.githubusercontent.com/102249128/201182797-a8deabb9-8e1b-4d30-a0cb-4f797db230aa.png)

First directory mysql server  and then 2nd in the image
then *execute* then next next 

On account and rules

Default acc

Root pass : password 

uncheck srartup option
next next and setup done

## Running it 
Search in command bar : Mysql 5.7 command line cient
type your passowrd which is thr *Root password*
now the server is live 

now do *create database *name*; *  #nickname=Giraffe

## Download *PopSQL*
 
 better for visualization of sql command 
 
 google search popsql and dwonload and sign in with google 
 connect to database
 
* Nickname: Giraffe
* Type: MySQL
* Hostname : localhost
* Port: 3306
* Database : Giraffe
* Username: root
* Password: password
 
 then connect and write queries

