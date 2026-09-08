# dbt
DBT_Ultimate_Guide

1. dbt core and dbt cli
2. dbt models
3. dbt jinja
4. dbt macros
5. dbt generic test and singular tests
6. dbt seeds
7. building scd's using snapshots
8. dbt node selection
9. dbt profiles
10. CI/CD workflows within DBT

What is DBT?
DBT - Data Build Tool

DBT is a transformation layer 

Pyspark does all most everything.
extracts, transforms, load, optimise and partitions 

Just the transformation part - you can use DBT

Why do we need DBT?
DBT provides you modularity or templating feature.

Lets say you have build a dwh, scd's, silver or gold layer.
In another business unit dwh, you did the same thing
In another business unit dwh, you did the same thing

You are doing the same thing again and again.

With DBT you can do that.
Define the code in one place, we use something called as templates (JINJA templates) and they make the code modular.
They do not write static code but dynamic code.

Earlier we used python list comprehensions, classes and functions to make our code dynamic. and it wasnt efficient.
Efficient way to perform it using dbt.
Features - scd, incremental loading Focused more on data engineering.

DBT platforms
1. DBT core - CLI TOOL (open source) you will need to manage it in terms of compute and git (ci/cd) (similar to apache spark)
2. DBT Cloud - Managed product build on top of dbt core (similar to databricks) - managed by DBT
3. DBT canvas - a feature available in dbt cloud. ( Has a dedicated tab - called canvas (template - drag and drop feature)

DBT Backbone - DBT MODELS
dbt models which hold your code (coding part of dbt) 
models will populate your data
Ex: two data engineer works in a team, they are using databricks or snowflake
They want to build bronze, silver and gold using dbt.
Lets say we have a source -> DBT (will use the source in dbt and cook something or build models and these models will populate data back to the platforms such as databricks, snowflake or synpase or redshift or bigquery or fabric.

Q. We need to compute to transform the code
Computation is provided by the platforms DB's, snowflake or synapse ....

DBT : i will transform your data or build your models or templates for you but in return i will use your resources.
Platform used here is: Databricks and install dbt core 
install python (dbt uses interpreter), install git (ci/cd) and UV (python package manager instead of pip)
code editor - VS code

Step 1: Databricks platform
Step 2: code editor (VS CODE)
Step 3: Git download (command prompt: git --version)
Step 4: Install Python (check python compatability for dbt) Also make sure to add python.exe to path

Create virtual environments for different projects
Before that lets install uv using pip
# pip install uv

Lets go to VS CODE
1. Create an empty folder
2. open the folder
3. Install an extension - python extension (support code hints, color changing properties)
4. terminal short cut - ctrl + shift + `

Lets create a virtual environment everything
you can download dbt package, but inorder to work efficiently you need to install package with respect to a virtual environment)
Terminal > traditionally we used: python -m venv .venv
with uv we dont need to write anything.
5. DBT core installation: downloading with package

Old school: creating virtual environment command: py -m venv env
create the package: dbt core and we cannot only install dbt core, we need an adaptor also.

We need a platform - for cluster compute and platform to process data (we need adaptor also).

Databricks adaptor, snowflake adaptor and so on.

VS code Terminal steps:
New approach create an virtual environment automatically: uv init
hidden files are created by uv and we dont need to worry about anything.
we need to be concerned only about .python-version (define the python version you want to use)

Q. where is our virtual environment?
It will be automatically created for you, the moment you run on one command: uv sync (make sure the python version is same) - .venv (it basically syncs all your properties defined in your code base)
we would need to install few libraries
earlier we used: pip install packagename
now: #uv add dbt-core
now install adaptor: # uv add dbt-databricks

Before uv we used to create some files called requirements.txt so we can store all our packages
Now how will we store everything?
Here in uv - we have pyproject.toml (stores all the packages (parent package name)

so we dont need to maintain requirements.txt as well :)
Thats why uv is amazing.

lets stay still we want to use requirements.txt because we want to use it
# uv pip freeze > requirements.txt

Q. download any dependencies written in requirements.txt
earlier: pip install -r requirements.txt
Now: uv add -r requirements.txt

Activate the virtual environment as well.

right now we have installed without activating the virtual environment.
so remove and activate and add
# uv remove dbt-core
# uv remove dbt-databricks

Make sure to activate it, .venv/Scripts/activate
Make sure to search - dbt

Git  Things
You dont need to do git init 
in the uv init (git init command is embedded)

# git branch -m main(renaming the master branch to main)
# git add .
# git commit -m "initial commit"

Lets set up source - Databricks 
catalog - dbt
schema - source
tables - refer source folder

Now, we will use dbt for transformation.

Lets start building models and initilaize dbt connection with databricks.
1. Project
2. Connection

Whenever you are using dbt cloud, all these things will be turned into nice UI.
# dbt command
dbt init
# enter a name for you project
dbt_priya 
> creates new folder with the given name, logs
# databricks or spark
1
# host name of databricks
SQL datawarehouse > connection details > hostname, http path

DBT will be using SQL warehouse 

 # access token 
 1
 # create a new token in databricks
 settings > developer > access tokens > generate new token > copy it
 # paste it in vs code

 # use unity catalog or no?
 1
 # catalog name?
 dbt
 #schema
 can type default, we will change the schema
 # thread
 1

 connection is established

 2nd dbt command
 # dbt debug

 # it says 1 check failed
 project.yml not found

 We are at parent folder but dbt project is present in project folder created
 cd priya_dbt_project

 # check dbt debug
 dbt debug

 # all checks passed

 One last things
 You see Using Profiles.yml file at c:\Users\priya\.dbt\profiles.yml
 Profile created for us and most important file for dbt core.
 Without this you cannot do anything.

 In this profiles.yml - yaml file all the connection details, tokens everything written.
 Q. Why created in c drive instead of project folder?
 by default it creates in project folder location also.
 We can anytime copy that file into that project folder.
 Whenever we run a dbt command - It first checks project folder and later c also.

 Ideally as a good developer, you should provide that file in the project folder.

 Lets explore project folder (DBT) - folder structure that we follow in dbt
 1. analyses
 2. logs
 3. macros
 4. models
 5. seeds
 6. snapshots
 7. tests
 8. .gitignore
 9. dbt_project.yml
 10. README.md
 

 NOTE: in dbt core whatever you do, you need to provide the metadata in dbt_project.yml 
 backbone of dbt core, whatever we provide here. it will go to that location and perform the stuff

 ex: model-paths: ["models"] models folder

 yml or yaml file - aint markup language or yet another markup language
 Format in that is YAML
 we cannot pick that format because we will be using JINJA templates.
 By default YAML Doesn't know, what is jinja template within yaml
 We need to tell it - we have many ways
 best way is: when doing local development that is dbt power or power user for dbt

 Q) what Power User extension does? makes coding better, auto complete your code, suggestions, lineage
 build graphs, build dags 
 all the features that are available in dbt cloud.

 click on dbt core button on vs code (left corner)
 select set up extension
 1. select python Interpreter
 2. Associated File Types (*.sql files needs to be associated with the value 'sql' or 'jinja-sql', *.yml file types should be associated with the value 'yaml' or 'jinja-yaml')
    > add Item - *.sql - jinja-sql
    > add Item - *.yml - jinja-yaml
    > ok

3. run dbt setups
4. finish setup

material icon theme extension

copy the file from c drive profiles (C:\Users\lohit\.dbt\profiles.yml) to this dbt project root

in dbt_project.yml -
You need to make sure that the profile is not set up as default.
It should be same name as your project and also in profiles.yml it should have same value 'priya_dbt_project'
It should be matching


let create a simple model
models folder - favourite folder 

we will create a medallian architecture
folders - 
models folder > bronze
              > silver
              > gold
              > source

We know that we want to populate the bronze layer
In bronze, we populate the data from the source as is

Simple code 
lets create a file > bronze_sales.sql

actually you want to create a bronze table in databricks
Q. I am in dbt, how can i create it?
No need to use CREATE TABLE syntax
Just select * from tablename





Lets go to databricks > source



 
 








