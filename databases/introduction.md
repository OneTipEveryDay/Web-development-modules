> in last project when save data (posts) inside a `var` when refresh site , you back to  primery page
> you need a data base to save your data
> types o f data base:
> > SQL‌ DB :‌ sql like a program language that allows you to sava data
> > NOSQL DB :   

exapmle a SQL database :
<img width="623" height="395" alt="image" src="https://github.com/user-attachments/assets/7f2cffe6-086e-4d7a-9ed8-83ae0e6d25d1" />
> i see a table have row and col
> note :‌ sql table have relationship between them
> have structure for planing and and guss relashenship betwwen tables

## SQL tutolrial for w3schools.com

### CRUD (create read update disreoy)

> you can practice in https://sqliteonline.com/

for ceate a table click on costomer.db right click on a table ans click `show table` and write this code
```
CREATE TABLE productsnum (
  idd INT NOT NULL,
  nam TEXT,
  PRICE MONEY,
  PRIMARY KEY(idd)
  )
```

for insert data click on INSERT and write
```
INSERT INTO table2 (column1, column2, column3, ...)
VALIUE v1 v3 v5;
```
















## postgreSQL (RDBMS) https://www.postgresql.org/docs/current/
> we have client in front side and hit to back end side . for handel requests we write index.js in server . inside index.js there is port  talk to database
> ,datatbase have user detales , information ,....
> in this module we see relationship between database and app(index.js)


this code for use postgresql : <br>
`npm install pg`


> The SQL CREATE TABLE Statement
```
CREATE TABLE table_name (
    column1 datatype,
    column2 datatype,
    column3 datatype,
   ....
);
```
query.sql:
```sql
CREATE TABLE capitals (
    id SERIAL PRIAMRY  KEY,
    country VARCHAR(45),
    capital VARCHAR(45)
   ....
);
```





















