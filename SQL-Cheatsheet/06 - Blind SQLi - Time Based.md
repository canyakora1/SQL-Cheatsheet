# Blind SQLi - Time Based

**Time-Based**
A time-based blind SQL injection is very similar to the above boolean-based one in that the same requests are sent, but there is no visual indicator of your queries being wrong or right this time. Instead, your indicator of a correct query is based on the time the query takes to complete. This time delay is introduced using built-in methods such as **SLEEP(x)** alongside the UNION statement. The SLEEP() method will only ever get executed upon a successful UNION SELECT statement. 

So, for example, when trying to establish the number of columns in a table, you would use the following query:

`admin123' UNION SELECT SLEEP(5);--`

If there was no pause in the response time, we know that the query was unsuccessful, so like on previous tasks, we add another column:

`admin123' UNION SELECT SLEEP(5),2;--`

This payload should have produced a 5-second delay, confirming the successful execution of the UNION statement and that there are two columns.

You can now repeat the enumeration process from the Boolean-based SQL injection, adding the SLEEP() method to the **UNION SELECT** statement.

If you're struggling to find the table name, the below query should help you on your way:

  
`referrer=admin123' UNION SELECT SLEEP(5),2 where database() like 'u%';--`