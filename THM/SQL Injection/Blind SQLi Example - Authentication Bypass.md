Unlike In-Band SQL injection, where we can see the results of our attack directly on the screen, blind SQLi is when we get little to no feedback to confirm whether our injected queries were, in fact, successful or not, this is because the error messages have been disabled, but the injection still works regardless. It might surprise you that all we need is that little bit of feedback to successfully enumerate a whole database.  

  

**Authentication Bypass**

One of the most straightforward Blind SQL Injection techniques is when bypassing authentication methods such as login forms. In this instance, we aren't that interested in retrieving data from the database; We just want to get past the login. 

  

Login forms that are connected to a database of users are often developed in such a way that the web application isn't interested in the content of the username and password but more in whether the two make a matching pair in the users table. In basic terms, the web application is asking the database, "Do you have a user with the username bob and the password bob123?" the database replies with either yes or no (true/false) and, depending on that answer, dictates whether the web application lets you proceed or not. 

  

Taking the above information into account, it's unnecessary to enumerate a valid username/password pair. We just need to create a database query that replies with a yes/true.

  

**Practical:**

Level Two of the SQL Injection examples shows this exact example. We can see in the box labelled "SQL Query" that the query to the database is the following:

  

`select * from users where username='%username%' and password='%password%' LIMIT 1;`

  

N.B The **%username%** and **%password%** values are taken from the login form fields. The initial values in the SQL Query box will be blank as these fields are currently empty.

  

To make this into a query that always returns as true, we can enter the following into the password field:

  

`' OR 1=1;--`

  

Which turns the SQL query into the following:

  

`select * from users where username='' and password='' OR 1=1;`

  

Because 1=1 is a true statement and we've used an **OR** operator, this will always cause the query to return as true, which satisfies the web applications logic that the database found a valid username/password combination and that access should be allowed.

**- Example**
Question #1: Log into the administrator account!  

After we navigate to the login page, enter some data into the email and password fields.

![](https://i.imgur.com/4XHHSof.png)

 Before clicking submit, make sure Intercept mode is on.

This will allow us to see the data been sent to the server!

  

![](https://i.imgur.com/6gyZ7Vr.png)  

  

We will now change the "**a**" next to the email to: ' or 1=1-- and forward it to the server.

![](https://i.imgur.com/tPFJnmC.png)

**Why does this work?**

1. The character **'** will close the brackets in the SQL query
2. '**OR**' in a SQL statement will return true if either side of it is true. As 1=1 is always true, the whole statement is true. Thus it will tell the server that the email is valid, and log us into user id 0, which happens to be the administrator account.
3. The -- character is used in SQL to comment out data, any restrictions on the login will no longer work as they are interpreted as a comment. This is like the # and // comment in python and javascript respectively.

  

                      ![](https://i.imgur.com/Y7xYGjp.png)

Question #2: Log into the Bender account!  

Similar to what we did in Question #1, we will now log into Bender's account! Capture the login request again, but this time we will put: bender@juice-sh.op'-- as the email. 

![](https://i.imgur.com/1F1ufc3.png)

Now, forward that to the server!  

But why don't we put the 1=1?

Well, as the email address is valid (which will return true), we do not need to force it to be true. Thus we are able to use **'--** to bypass the login system. Note the **1=1** can be used when the email or username is not known or invalid.

                     ![[Pasted image 20240621185902.png]]
