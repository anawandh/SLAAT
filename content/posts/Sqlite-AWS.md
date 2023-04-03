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

### Change your init.py file to this --

``` from flask import Flask
from flask_login import LoginManager
from flask_sqlalchemy import SQLAlchemy
from flask_migrate import Migrate

"""
These object can be used throughout project.
1.) Objects from this file can be included in many blueprints
2.) Isolating these object definitions avoids duplication and circular dependencies
"""

# Setup of key Flask object (app)
app = Flask(__name__)

# Setup SQLAlchemy object and properties for the database (db)
dbURI = 'postgresql+psycopg2://<postgres>:<nighthawk>@<test-database-adi.ctenoof0kzic.us-east-2.rds.amazonaws.com>:<5432>/<test-database-adi>'

app.config['SQLALCHEMY_TRACK_MODIFICATIONS'] = False
app.config['SQLALCHEMY_DATABASE_URI'] = dbURI
app.config['SECRET_KEY'] = 'SECRET_KEY'
db = SQLAlchemy(app)
Migrate(app, db)

# Images storage
app.config['MAX_CONTENT_LENGTH'] = 5 * 1024 * 1024  # maximum size of uploaded content
app.config['UPLOAD_EXTENSIONS'] = ['.jpg', '.png', '.gif']  # supported file types
app.config['UPLOAD_FOLDER'] = 'volumes/uploads/'  # location of user uploaded content 
```

### To create a RDS database file 

- First create a database in RDS service
    - Steps:
    > - go to dashboard of AWS, go to search bar and type RDS, click on the first thing that pops up
    > - Create your own instance, make sure to remember the master password. use default security group and connect to an ec2 instance that you want the database in. 
    > - Change your init.py file with this config -
        dbURI = 'postgresql+psycopg2://<username>:<password>@<host>:<port>/<database_name>' 

- here 
    - Username: master username
    - Password: master password
    - Host: host id can be found in the configuration tab of the instance
    - Port: port of the database
    - Database name: the database name

This is what the instance once created will look like
![image](https://user-images.githubusercontent.com/108041389/229413905-09da8795-6846-4c3c-8c2a-219924f1363b.png)
- Upon clicking on the instance name you can find the configuration file.
- ![image](https://user-images.githubusercontent.com/108041389/229414099-4a6e65fa-097a-42bc-bdfc-d043847b27b4.png)