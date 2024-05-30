# SQL

SQL (Structured Query Language) is a feature-rich language used for querying databases. These SQL queries are better referred to as statements.  

The simplest of the commands which we'll cover in this task is used to retrieve (select), update, insert and delete data. Although somewhat similar, some database servers have their own syntax and slight changes to how things work. All of these examples are based on a MySQL database. After learning the lessons, you'll easily be able to search for alternative syntax online for the different servers. It's worth noting that SQL syntax is not case-sensitive.

---

## SELECT
The first query type we'll learn is the SELECT query used to retrieve data from the database. 

`select * from users;`

|   |   |   |
|---|---|---|
|**id**|**username**|**password**|
|1|jon|pass123|
|2|admin|p4ssword|
|3|martin|secret123|

The first word ``SELECT``, tells the database we want to retrieve some data; the * tells the database we want to receive back all columns from the table. For example, the table may contain three columns (id, username and password). "from users" tells the database we want to retrieve the data from the table named users. Finally, the semicolon at the end tells the database that this is the end of the query.  



The next query is similar to the above, but this time, instead of using the * to return all columns in the database table, we are just requesting the username and password field.

`select username,password from users;`

|   |   |
|---|---|
|**username**|**password**|
|jon|pass123|
|admin|p4ssword|
|martin|secret123|

The following query, like the first, returns all the columns by using the * selector, and then the "LIMIT 1" clause forces the database to return only one row of data. Changing the query to "LIMIT 1,1" forces the query to skip the first result, and then "LIMIT 2,1" skips the first two results, and so on. You need to remember the first number tells the database how many results you wish to skip, and the second number tells the database how many rows to return.

`select * from users LIMIT 1;`

|   |   |   |
|---|---|---|
|**id**|**username**|**password**|
|1|jon|pass123|

Lastly, we're going to utilize the where clause; this is how we can finely pick out the exact data we require by returning data that matches our specific clauses:

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

This will only return the rows where the username is either equal to **admin** or **j****on**. 

`select * from users where username='admin' and password='p4ssword';`

|   |   |   |
|---|---|---|
|**id**|**username**|**password**|
|2|admin|p4ssword|

This will only return the rows where the username is equal to **admin** and the password is equal to **p4ssword**.

Using the like clause allows you to specify data that isn't an exact match but instead either starts, contains or ends with certain characters by choosing where to place the wildcard character represented by a percentage sign %.

`select * from users where username like 'a%';`

|   |   |   |
|---|---|---|
|**id**|**username**|**password**|
|2|admin|p4ssword|

This returns any rows with a username beginning with the letter a.

`select * from users where username like '%n';`

|   |   |   |
|---|---|---|
|**id**|**username**|**password**|
|1|jon|pass123|
|2|admin|p4ssword|
|3|martin|secret123|

This returns any rows with a username ending with the letter n.

`select * from users where username like '%mi%';`

|   |   |   |
|---|---|---|
|**id**|**username**|**password**|
|2|admin|p4ssword|

This returns any rows with a username containing the characters **mi** within them.

---

## UNION

The UNION statement combines the results of two or more SELECT statements to retrieve data from either single or multiple tables; the rules to this query are that the UNION statement must retrieve the same number of columns in each SELECT statement, the columns have to be of a similar data type, and the column order has to be the same. This might sound not very clear, so let's use the following analogy. Say a company wants to create a list of addresses for all customers and suppliers to post a new catalogue. We have one table called customers with the following contents:  


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

Using the following SQL Statement, we can gather the results from the two tables and put them into one result set:

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

---

## INSERT

The **INSERT** statement tells the database we wish to insert a new row of data into the table. **"into users"** tells the database which table we wish to insert the data into, **"(username,password)"** provides the columns we are providing data for and then **"values ('bob','password');"** provides the data for the previously specified columns.

`insert into users (username,password) values ('bob','password123');`

|   |   |   |
|---|---|---|
|**id**|**username**|**password**|
|1|jon|pass123|
|2|admin|p4ssword|
|3|martin|secret123|
|4|bob|password123|

---

## UPDATE

The **UPDATE** statement tells the database we wish to update one or more rows of data within a table. You specify the table you wish to update using "**update %tablename% SET**" and then select the field or fields you wish to update as a comma-separated list such as "**username='root',password='pass123'**" then finally, similar to the SELECT statement, you can specify exactly which rows to update using the where clause such as "**where username='admin;**".

`update users SET username='root',password='pass123' where username='admin';`

|   |   |   |
|---|---|---|
|**id**|**username**|**password**|
|1|jon|pass123|
|2|root|pass123|
|3|martin|secret123|
|4|bob|password123|

---

## DELETE

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

