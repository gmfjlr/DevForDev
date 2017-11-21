---
layout: documentation
category: Sql
title: T-SQL Development
order: 3
---

IF you write bad SQL Code, be ready to face the performance issues. So SQL Code should be written by dedicated sql programmers. Good experienced sql developers can write very good sql code, which will definitely improve the performance of the database. So write your SQL code with SQL Experts.

### Best Practices
  
  - Don´t use `select * from tablename` instead write selected column names.Example: `Select col1, col2 from tablename`.
  - Use comments for each block of code.
  - Don´t use `SP_` while naming your Procedure (Learn From here).
  - Use `CTE` Common table Expression instead of temporary tables. `CTE` scope is limited to the next statement in the query. [Learn From here](https://www.codeproject.com/articles/265371/common-table-expressions-cte-in-sql-server).
  - Use `SET NOCOUNT ON` in the procedures. This will really improve the performance.
  - Avoid using `cursors` in Procedures, rather use `case` statement, `while loop` or `Merge` clause.
  - Don´t use `Recompile` option in stored procedure.
  - While working with complicated logics use parenthesis to improve the readability.
  - Try to avoid cross joins.
  - Use `IF Exists` rather than `count (*)` for data existence in table.
  - Don´t query data from Application side, instead use stored procedures.
  - Don´t use store Images in the database, rather use File streams.
  - Try to avoid dynamic SQL, since it is slower than Static SQL. [Learn From here](http://www.sqlservercentral.com/articles/Security/dynamicsqlversusstaticsqlp1/617/)
  - Always use column names in insert statement.
  - Use `Union` only if required otherwise use `Union all`.
  - Use `Except` and `Not Exists` Instead of `Left Join` and `Not In`.
  - Use `sp_executesql` instead of `Exec(@str)` for the execution of dynamic sql.
  - Design Indexes effectively and make sure that created indexes are used by the queries. Don’t make too much indexes in a table.
  - Use Merge operator for multiple DML operations `Insert`, `Update`, `Delete`. [Learn From here](https://docs.microsoft.com/en-us/sql/t-sql/statements/merge-transact-sql).
  - Use policy management to enforce for configuring and managing SQL Server across the organization.
  - Use `Try Catch` for Error handling.

We recomend to visit this both links to learn more functionality about Querying SQL Server 2012.

  - [Part 1](https://www.codeproject.com/articles/690340/querying-sql-server-part-i).
  - [Part 2](https://www.codeproject.com/articles/692269/querying-sql-server-part-ii).

### Naming Conventions and Format

  - T-SQL Code has a format with indents. You can use below website to format queries. [Formater](http://www.dpriver.com/pp/sqlformat.htm).

Write like this

```sql
  SELECT 
      a.Column2, b.Column2 
  FROM 
      dbo.TableName1 a
          JOIN dbo.TableName2 b ON
              a.Column1 = b.Column1
  WHERE
      a.Column3 = 1
```

Not like this

```sql  
  SELECT a.Column2, b.Column2 FROM dbo.TableName1 a JOIN dbo.TableName2 b ON a.Column1 = b.Column1 WHERE a.Column3 = 1
```

  - Avoid using spaces in the sql server objects. Example:

Use

```sql
  SELECT * FROM dbo.EmployeeDetails
```

Don´t use

```sql
  SELECT * FROM dbo.[Employee Details]
```

  - Use usp_ prefix for stored procedures.
  - Use fn_ prefix for functions.
  - Specify the schema name in the table names. Example: 
  
```sql
  SELECT * FROM dbo.EmployeeDetails
```

### Script Comments

This is the most important act of the developer when is writting code, this helps to identify and understand the main activities of the script, you must comment everything that is important:
  
  - **Single line comment**: This represents a single line comment using `--`.
  - **Multiple line comment**: This represents block of lines of comments using `/* . . . */`.
  
There are some template to achieve this:

  - Store Procedures
  - Functions
