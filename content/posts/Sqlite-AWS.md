---
title: SQlite --> AWS databse
description: NGINX configuration for APCSP
date: 2023-03-24
draft: false
featured_image: "/images/notebook.jpg"
description: ""
---

## Background

> - You can use AWS Database Migration Service (AWS DMS) to migrate your data to and from most widely used commercial and open-source databases such as Oracle, PostgreSQL, Microsoft SQL Server, Amazon Redshift, Amazon Aurora, MariaDB, and MySQL.
> - AWS DMS allows you to use SQLite operators and SQLite functions within a transformation rule to compute column values that you can apply to any selected schema, table, or view. In addition, AWS DMS supports expressions, which means using SQLite operators or functions to define the data in a column

![image](https://user-images.githubusercontent.com/108041389/227831084-10ab2eb9-bb51-42c4-bdab-4620ba315898.png)

### RDS on AWS looks like this 
![image](https://user-images.githubusercontent.com/108041389/229413905-09da8795-6846-4c3c-8c2a-219924f1363b.png)
- The picture above shows an RDS instance that has been made. 

### To create a RDS database file 

- First create a database in RDS service
    - Steps:
    > - go to dashboard of AWS, go to search bar and type RDS, click on the first thing that pops up
    > - go to easy create, name the database whatever you want and choose PostgresSQL as your RDS engine. and then folllow instructions on this page [link](https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/CHAP_GettingStarted.CreatingConnecting.PostgreSQL.html)
    > - Create your own instance, make sure to remember the master password. use default security group and connect to an ec2 instance that you want the database in. 

This is what the instance once created will look like
![image](https://user-images.githubusercontent.com/108041389/229413905-09da8795-6846-4c3c-8c2a-219924f1363b.png)
- Upon clicking on the instance name you can find the configuration file.
- ![image](https://user-images.githubusercontent.com/108041389/229414099-4a6e65fa-097a-42bc-bdfc-d043847b27b4.png)


### Connecting to an EC2 
in the same link as above - [link](https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/CHAP_GettingStarted.CreatingConnecting.PostgreSQL.html)
we can find the instructions to make the ec2 instance and connecting it to the RDS instance that you created now we are ready to play around. 
run the following code segments:
``` 
sudo yum update -y 

```
- this updates dependencies if needed
```
sudo amazon-linux-extras install postgresql14
```
- installs postgres engine to run postgres commands 
> - note* for the ec2 that you will use for hacks, yu do not need to run this command as I have done them for you

----
### needed
```
psql --host=database-test1.ctenoof0kzic.us-east-2.rds.amazonaws.com --port=5432 --username=postgres
```
- Once you reach this step, if it asks for password - ask me!
- The password is - Aditya123

Now you have logged into the RDS as the creator who has all the rights

## Postgres Commands
- to see all the tables in the instance the command is - 
```
\l
```

- to create database -
```
CREATE DATABASE (type the database name you want- do not include the parenthesis)
```

- to connect to created database
```
\c databse_name 
```

Create a table
```
CREATE TABLE ADI (
  ID INT PRIMARY KEY NOT NULL,
  NAME TEXT NOT NULL,
  CLASS TEXT NOT NULL
);

```
make a query to add data
- More commands here - [Command link](https://www.tutorialspoint.com/postgresql/postgresql_create_table.htm)
- hint: go to the link and find the tab that says "Insert Query" on the left side of the page

## Hacks
- Create your own database in the EC2 I have created (ec2-database-connect)
    - name it with your first and last name (example:  aditya-nawandhar)
    - Create a table using the commands on the link provided.
    - using commands from the link provided make columns and rows with test data (can be anything) (example: "name" and "class" are the columns with rows being something like "Aditya" and "Junior"). At least 4 test rows.
    - Hint: to add test data use query's
    - additional points if the data matches CPT
