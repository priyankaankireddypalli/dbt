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








