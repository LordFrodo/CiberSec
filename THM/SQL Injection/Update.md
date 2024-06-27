The **UPDATE** statement tells the database we wish to update one or more rows of data within a table. You specify the table you wish to update using "**update %tablename% SET**" and then select the field or fields you wish to update as a comma-separated list such as "**username='root',password='pass123'**" then finally, similar to the SELECT statement, you can specify exactly which rows to update using the where clause such as "**where username='admin;**".

  

`update users SET username='root',password='pass123' where username='admin';`

  

|        |              |              |
| ------ | ------------ | ------------ |
| **id** | **username** | **password** |
| 1      | jon          | pass123      |
| 2      | root         | pass123      |
| 3      | martin       | secret123    |
| 4      | bob          | password123  |