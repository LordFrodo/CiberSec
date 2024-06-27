The **DELETE** statement tells the database we wish to delete one or more rows of data. Apart from missing the columns you wish to return, the format of this query is very similar to the SELECT. You can specify precisely which data to delete using the **where** clause and the number of rows to be deleted using the **LIMIT** clause.

  

`delete from users where username='martin';`

|   |   |   |
|---|---|---|
|**id**|**username**|**password**|
|1|jon|pass123|
|2|root|pass123|
|4|bob|password123|

`delete from users;`

  

Because no WHERE clause was being used in the query, all the data was deleted from the table.  

|   |   |   |
|---|---|---|
|**id**|**username**|**password**|