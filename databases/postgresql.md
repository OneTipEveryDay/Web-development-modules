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

## how to connect database to backend
###‌ for emplemented node and backend take few steps 

>‌ 1. install pg npm package
> 2. create index.js
> 3. import pg from "pg"
> 4. const db = new pg.Client(....);
> 5. db.connect();
> 6. choise a table from database  db.query(....);
> 7.  de.end();

# quiz example from capitals 

> -mkdir a dir
> -import capitals.csv
> create imdex.js  ,....

index.js
```js
import express from "express";
import bodyParser from "body-parser";
import pg from "pg";

const db = new pg.Client({
  user: "postgres",
  host: "localhost",
  database: "databasename",
  password: "your password",
  port: 5432,
});

const app = express();
const port = 3000;

db.connect();

let quiz = [];
db.query("SELECT * FROM capitals", (err, res) => {
  if (err) {
    console.error("Error executing query", err.stack);
  } else {
    quiz = res.rows;
  }
  db.end();
});

let totalCorrect = 0;

// Middleware
app.use(bodyParser.urlencoded({ extended: true }));
app.use(express.static("public"));

let currentQuestion = {};

// GET home page
app.get("/", async (req, res) => {
  totalCorrect = 0;
  await nextQuestion();
  console.log(currentQuestion);
  res.render("index.ejs", { question: currentQuestion });
});

// POST a new post
app.post("/submit", (req, res) => {
  let answer = req.body.answer.trim();
  let isCorrect = false;
  if (currentQuestion.capital.toLowerCase() === answer.toLowerCase()) {
    totalCorrect++;
    console.log(totalCorrect);
    isCorrect = true;
  }

  nextQuestion();
  res.render("index.ejs", {
    question: currentQuestion,
    wasCorrect: isCorrect,
    totalScore: totalCorrect,
  });
});

async function nextQuestion() {
  const randomCountry = quiz[Math.floor(Math.random() * quiz.length)];
  currentQuestion = randomCountry;
}

app.listen(port, () => {
  console.log(`Server is running at http://localhost:${port}`);
});

```

index.ejs
```
<!DOCTYPE html>
<html lang="en">

<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Capital City Quiz</title>
  <link rel="stylesheet" href="/styles/main.css">
</head>

<body id="app">
  <form class="container" action="/submit" method="post">
    <div class="horizontal-container">
      <h3>
        Total Score:
        <span id="score">
          <%= locals.totalScore ? totalScore : "0" %>
        </span>
      </h3>

    </div>

    <h1 id="countryName">
      <%=question.country %>
    </h1>
    <div class="answer-container">
      <input type="text" name="answer" id="userInput" placeholder="Enter the capital" autofocus autocomplete="off">

    </div>
    <button type="submit">SUBMIT<% if(locals.wasCorrect){ %>
        <span class="checkmark">✔</span>
        <% } else if (locals.wasCorrect===false) { %>
          <span class="cross" id="error">✖</span>
          <% } %>
    </button>

  </form>
  <script>
    var wasCorrect = "<%= locals.wasCorrect %>";
    console.log(wasCorrect)
    if (wasCorrect === "false") {
      alert('Game over! Final best score: <%= locals.totalScore %>');
      document.getElementById("app").innerHTML = '<a href="/" class="restart-button">Restart</a>'
    }


  </script>
</body>

</html>
```

style.css

```css
body {
  background-image: url(../images/background.jpg);
  background-repeat: no-repeat;
  background-size: cover;
  font-family: Arial, sans-serif;
}

.container {
  display: flex;
  flex-direction: column;
  justify-content: space-evenly;
  max-width: 40%;
  height: 300px;
  margin: 15% auto;
  padding: 20px;
  background-color: #fff;
  border-radius: 10px;
  box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
  padding-top: 10px;
}

h1 {
  text-align: center;
}

h3 {
  margin: 0;
}

.answer-container {
  width: 100%;
  text-align: center;
}

input {
  text-align: center;
  width: 30%;
  margin: 10px auto;
  padding: 10px;
  border: 1px solid #ccc;
  border-radius: 5px;
}

button {
  font-weight: 800;
  letter-spacing: 2px;
  font-size: large;
  display: block;
  width: 100%;
  padding: 10px;
  background-color: #ffca00;
  color: white;
  border: none;
  border-radius: 5px;
  cursor: pointer;
}

.horizontal-container {
  display: flex;
  justify-content: space-between;
}

button:hover {
  background-color: #ffd500;
}

#result {
  text-align: center;
  font-size: 24px;
}

.checkmark {
  color: transparent;
  animation: checkmark 0.5s ease;
}

.cross {
  color: transparent;
  animation: cross 0.5s ease;
}

@keyframes checkmark {
  0% {
    color: transparent;
  }
  100% {
    color: green;
  }
}

@keyframes cross {
  0% {
    color: transparent;
  }
  100% {
    color: red;
  }
}

.restart-button {
  display: inline-block;
  background-color: #fff;
  color: #333;
  padding: 15px 30px;
  font-size: 18px;
  text-align: center;
  text-decoration: none;
  border-radius: 30px;
  box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
  transition: background-color 0.3s, color 0.3s;
}

```
background image
<img width="2000" height="2000" alt="image" src="https://github.com/user-attachments/assets/066c04d7-12c1-443d-9a5e-f8879b3b25d6" />

### for more develope example look at templates EJS 
....

## query data using WHERE and LIKE
### food world example
> 1.create a table in pgadmin name world-food look at world-food.csv and create col like that 

```
CREATE TABLE food_world (
	id SERIAL PRIMARY KEY,
	country VARCHAR(45),
	rice_production FLOAT,
	wheat_production FLOAT
);
```
>[!ERROR]
>  csv file dont have id col when you import it make shore click on to x
>id will generated serial


> 2. select eveything from table (write in query tool ) (how?)
> 3. select one column `SELECT COLNAME FROM TABLENAME`
> 4. select multi  column `SELECT COLNAME1, colname2 FROM TABLENAME`
> 5. for check a condition : `SELECT COLNAME FROM TABLENAME WHERE CONDITION;`
> 6. EXAMPLE: SELECT rice_producion FROM food_world WHERE country= 'United States';
> 7. for check matching things `SELECT COLNAME FROM TABLENAME WHERE COLNAME LIKE pattern;`
> 8. for example `united states ` and  ` united states of america`
> 9. example : SELECT country FROM food_world WHERE country  LIKE 'U' || '%';


## doing cool exersise travel tracker
...



# insert data to table
``` INSERT INTO TABLE (COL1, COL2) VALUES (VAL1, VAL2) ```
``` db.query(INSERT INTO TABLE (COL1, COL2) VALUES (VAL1, VAL2) , ["italy", 2.541]) ```

# relationship types

<img width="891" height="537" alt="image" src="https://github.com/user-attachments/assets/605e0287-ef52-486b-9906-944fd48a6268" />

## one to one
```
CREATE TABLE student (
    id INT PRIMARY KEY,
    fname VARCHAR(50) ,
    lname VARCHAR(50));

CREATE TABLE cantact_detals (
    id INT PRIMARY KEY,
    address TEXT,
    mager VARCHAR(50)
    );
```
how to use : 

```
SELECT *
FROM student
JOIN contact_detals
ON student.id = contact_detals.id
```
output show me two table with 1 col  that `JOIN` together and build one table

## one to many
<img width="1329" height="489" alt="image" src="https://github.com/user-attachments/assets/ff4083de-cba7-4bde-991f-91f5cbda1d58" />

```
CREATE TABLE student (
    id SERIAL PRIMARY KEY,
    fname VARCHAR(50) ,
    lname VARCHAR(50));

CREATE TABLE htmeworks (
    id SERIAL PRIMARY KEY,
    mark INTEGER ,
    student_id INTEGER REFERENCES student(id)
);



```
> student_id INTEGER REFERENCES student(id) line actuely is this
> student_id INTEGER REFERENCES TABLENAKE(FIELD)

```
SELECT *
FROM student
JOIN HOMEWORK
ON student.id = student_id
```

OUTPUT WILL BE:
<img width="772" height="244" alt="image" src="https://github.com/user-attachments/assets/45b687f5-13a2-4253-8988-e8877c41ee44" />

## many to many
























