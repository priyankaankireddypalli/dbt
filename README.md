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









