The first query type we'll learn is the SELECT query used to retrieve data from the database. 

   

`select * from users;`

  

|   |   |   |
|---|---|---|
|**id**|**username**|**password**|
|1|jon|pass123|
|2|admin|p4ssword|
|3|martin|secret123|

The first-word SELECT tells the database we want to retrieve some data, the * tells the database we want to receive back all columns from the table. For example, the table may contain three columns (id, username and password). "from users" tells the database we want to retrieve the data from the table named users. Finally, the semicolon at the end tells the database that this is the end of the query.  

  

The next query is similar to the above, but this time, instead of using the * to return all columns in the database table, we are just requesting the username and password field.

  

`select username,password from users;`

  

|   |   |
|---|---|
|**username**|**password**|
|jon|pass123|
|admin|p4ssword|
|martin|secret123|

The following query, like the first, returns all the columns by using the * selector and then the "LIMIT 1" clause forces the database only to return one row of data. Changing the query to "LIMIT 1,1" forces the query to skip the first result, and then "LIMIT 2,1" skips the first two results, and so on. You need to remember the first number tells the database how many results you wish to skip, and the second number tells the database how many rows to return.

  

`select * from users LIMIT 1;`

  

|   |   |   |
|---|---|---|
|**id**|**username**|**password**|
|1|jon|pass123|

Lastly, we're going to utilise the where clause; this is how we can finely pick out the exact data we require by returning data that matches our specific clauses:

  

`select * from users where username='admin';`

  

|   |   |   |
|---|---|---|
|**id**|**username**|**password**|
|2|admin|p4ssword|

This will only return the rows where the username is equal to admin.

  

`select * from users where username != 'admin';`

  

|   |   |   |
|---|---|---|
|**id**|**username**|**password**|
|1|jon|pass123|
|3|martin|secret123|

This will only return the rows where the username is **NOT** equal to admin.

  

`select * from users where username='admin' or username='jon';`

  

|   |   |   |
|---|---|---|
|**id**|**username**|**password**|
|1|jon|pass123|
|2|admin|p4ssword|

This will only return the rows where the username is either equal to **admin** or j**on**. 

  

`select * from users where username='admin' and password='p4ssword';`

  

|   |   |   |
|---|---|---|
|**id**|**username**|**password**|
|2|admin|p4ssword|

This will only return the rows where the username is equal to **admin**, and the password is equal to **p4ssword**.

  

Using the like clause allows you to specify data that isn't an exact match but instead either starts, contains or ends with certain characters by choosing where to place the wildcard character represented by a percentage sign %.

  

`select * from users where username like 'a%';`

  

|   |   |   |
|---|---|---|
|**id**|**username**|**password**|
|2|admin|p4ssword|

This returns any rows with username beginning with the letter a.

  

`select * from users where username like '%n';`

  

|   |   |   |
|---|---|---|
|**id**|**username**|**password**|
|1|jon|pass123|
|2|admin|p4ssword|
|3|martin|secret123|

This returns any rows with username ending with the letter n.

  

`select * from users where username like '%mi%';`

  

|   |   |   |
|---|---|---|
|**id**|**username**|**password**|
|2|admin|p4ssword|

This returns any rows with a username containing the characters **mi** within them.