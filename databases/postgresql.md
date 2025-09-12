after half dey i see pgadmin filtered and i need a vpn (just hello dear iran)
<br>
> after build a password for postgres acount and log in to pgadmin
> right click in database (postgres ) and create a database [ i named world]
> and now i want create  a table (capitals):
> 1. select Query tool to write SQL code
> 2. write your code
> 3. run
> 4. refresh Tables on datsbase icon
> 5. view/Edit data / all rows

### import your data 

> 1. right click on table(capitals) and click import export data
> 2. imoirt file.csv
> 3. option tab and enable Header
> 4. most most table clomn names ====   col names in sql code
> 5. ok
> 6. if your names not equal go to perapertis click on and go to col edit col name
> 7. right click on Tables and Refresh
> 8. go view/Edit data / all rows
> 9. 

### read from a postgres database
sql read code 
```sql
SELECT * FROM <name of table>
```
for emplemented node and backend take few steps :

>‌ 1. install pg npm package
> 2. create index.js
> 3. import pg from "pg"
> 4. const db = new pg.Client(....);
> 5. db.connect();
> 6. choise a table from database  db.query(....);
> 7.  de.end();




















