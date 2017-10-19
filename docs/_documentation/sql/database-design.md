---
layout: documentation
category: Sql
title: Database Design
order: 2
---

## Database Design

### Important Recomendation

Database design is the critical part of any application. Developing software without a proper database design is similar to building a Multi-storied building with no proper foundation. Multi-storied building will collapse once it is occupied or some floors are added to the existing building. The same scenario will happen here also. So database design need to be done by database experts who have relevant experience desired database server. This is because Oracle and MS SQL Server has different architectures internally. Here we are discussing about OLTP database.

### Best Practices

  - Database should be normalized to minimum 3rd level normal form. Please do de-normalization if required.
  - Choose Right Data types for the columns.
  - Enforce foreign key constraints.
  - Each table should at least contain a clustered key.
  
### Naming Conventions

  - **Tables/Procedures/views**: Use Pascal Notations for SQL Server objects like Tables, Procedures and views. For e.g.: EmployeeDetails.
  - **Primary Key**: Use Pk_<table_name> for Primary key. Eg: PK_ EmployeeDetails.
  - **Non Clustered Index**: Create IX_<table_name>_<column1>_...<columnN>, where column1 to column N are columns used in the index.
  - **Default**: Example: DF_<table_name>_<column_name>
  
