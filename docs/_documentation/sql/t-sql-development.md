---
layout: documentation
category: Sql
title: T-SQL Development
order: 3
---

IF you write bad SQL Code, be ready to face the performance issues. So SQL Code should be written by dedicated sql programmers. Good experienced sql developers can write very good sql code, which will definitely improve the performance of the database. So write your SQL code with SQL Experts.

### Best Practices
  
  - Don’t use `select * from tablename` instead write selected column names.Example: `Select col1, col2 from tablename`.
  - Use comments for each block of code.
  - Don’t use `SP_` while naming your Procedure (Learn From here).
  - Use `CTE` Common table Expression instead of temporary tables. `CTE` scope is limited to the next statement in the query. (Learn From here)
  - Use `SET NOCOUNT ON` in the procedures. This will really improve the performance.
  - Avoid using `cursors` in Procedures, rather use `case` statement, `while loop` or `Merge` clause.
  - Don’t use `Recompile` option in stored procedure.
  - While working with complicated logics use parenthesis to improve the readability.
  - Try to avoid cross joins.
  - Use `IF Exists` rather than `count (*)` for data existence in table.
  - Don’t query data from Application side, instead use stored procedures.
  - Don’t use store Images in the database, rather use File streams.
  - Try to avoid dynamic SQL, since it is slower than Static SQL.SQL SERVER GUIDELINES-SQLINFO January 2, 2012Varun R | Database Administrator |www.sqlinfo.in|An i-book for SQL Server by Varun R Page 5
  - Always use column names in insert statement.
  - Use `Union` only if required otherwise use `Union all`.
  - Use `Except` and `Not Exists` Instead of Left join and Not in- Use `sp_executesql` instead of `Exec(@str)` for the execution of dynamic sql.
  - Design Indexes effectively and make sure that created indexes are used by the queries. Don’t make too much indexes in a table.
  - Use Merge operator for multiple DML operations `Insert`, `Update`, `Delete`. (Learn From here)
  - Use policy management to enforce for configuring and managing SQL Server across the organization.
  - Use `Try Catch` for Error handling.
