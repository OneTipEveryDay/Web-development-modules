> JavaScript Object Notation (JSON) is a standard text-based format for representing structured data based on JavaScript object syntax. 
> It is commonly used for transmitting data in web applications .

# JSON structure
<p>
 The following is a valid JSON string representing an object. Note that it is also a valid JavaScript object literal — just with some more syntax restrictions.
</p>
 ```json
{
  "squadName": "Super hero squad",
  "homeTown": "Metro City",
  "formed": 2016,
  "secretBase": "Super tower",
  "active": true,
  "members": [
    {
      "name": "Molecule Man",
      "age": 29,
      "secretIdentity": "Dan Jukes",
      "powers": ["Radiation resistance", "Turning tiny", "Radiation blast"]
    },
    {
      "name": "Madame Uppercut",
      "age": 39,
      "secretIdentity": "Jane Wilson",
      "powers": [
        "Million tonne punch",
        "Damage resistance",
        "Superhuman reflexes"
      ]
    },
    {
      "name": "Eternal Flame",
      "age": 1000000,
      "secretIdentity": "Unknown",
      "powers": [
        "Immortality",
        "Heat Immunity",
        "Inferno",
        "Teleportation",
        "Interdimensional travel"
      ]
    }
  ]
}
```

<p>
If you load this JSON in your JavaScript program as a string, you can parse it into a normal object and then access the data inside it using the same dot/bracket notation we looked at in the JavaScript object basics article. For example:
</p>

```
superHeroes.homeTown;
superHeroes.members[1].powers[2];
```

<p>
First, we have the variable name — superHeroes.
Inside that, we want to access the members property, so we use .members.
members contains an array populated by objects. We want to access the second object inside the array, so we use [1].
Inside this object, we want to access the powers property, so we use .powers.
Inside the powers property is an array containing the selected hero's superpowers. We want the third one, so we use [2].
</p>


## Arrays as JSON

We can also convert arrays to/from JSON. The below example is perfectly valid JSON:

```js
[
  {
    "name": "Molecule Man",
    "age": 29,
    "secretIdentity": "Dan Jukes",
    "powers": ["Radiation resistance", "Turning tiny", "Radiation blast"]
  },
  {
    "name": "Madame Uppercut",
    "age": 39,
    "secretIdentity": "Jane Wilson",
    "powers": [
      "Million tonne punch",
      "Damage resistance",
      "Superhuman reflexes"
    ]
  }
]
```
You have to access array items (in its parsed version) by starting with an array index, for example superHeroes[0].powers[0]. <br>

The JSON can also contain a single primitive. For example, 29, "Dan Jukes", or true are all valid JSON.


## Working through a JSON example
create index.html and style.css :
```html
<header>
...
</header>

<section>
...
</section>

<script>
// JavaScript goes here
</script>
```
i mean :
```
<!DOCTYPE html>
<html lang="en-US">
  <head>
    <meta charset="utf-8">

    <title>Our superheroes</title>

    <link href="https://fonts.googleapis.com/css?family=Faster+One" rel="stylesheet">
    <link rel="stylesheet" href="style.css">
  </head>

  <body>

      <header>

      </header>

      <section>

      </section>

      <script>

      </script>
  </body>
</html>
```

```css

/* || general styles */

html {
  font-family: 'helvetica neue', helvetica, arial, sans-serif;
}

body {
  width: 800px;
  margin: 0 auto;
}

h1, h2 {
  font-family: 'Faster One', cursive;
}

/* header styles */

h1 {
  font-size: 4rem;
  text-align: center;
}

header p {
  font-size: 1.3rem;
  font-weight: bold;
  text-align: center;
}

/* section styles */

section article {
  width: 33%;
  float: left;
}

section p {
  margin: 5px 0;
}

section ul {
  margin-top: 0;
}

h2 {
  font-size: 2.5rem;
  letter-spacing: -5px;
  margin-bottom: 10px;
}
```

We have made our JSON data available on our GitHub:

```json
{
  "squadName" : "Super Hero Squad",
  "homeTown" : "Metro City",
  "formed" : 2016,
  "secretBase" : "Super tower",
  "active" : true,
  "members" : [
    {
      "name" : "Molecule Man",
      "age" : 29,
      "secretIdentity" : "Dan Jukes",
      "powers" : [
        "Radiation resistance",
        "Turning tiny",
        "Radiation blast"
      ]
    },
    {
      "name" : "Madame Uppercut",
      "age" : 39,
      "secretIdentity" : "Jane Wilson",
      "powers" : [
        "Million tonne punch",
        "Damage resistance",
        "Superhuman reflexes"
      ]
    },
    {
      "name" : "Eternal Flame",
      "age" : 1000000,
      "secretIdentity" : "Unknown",
      "powers" : [
        "Immortality",
        "Heat Immunity",
        "Inferno",
        "Teleportation",
        "Interdimensional travel"
      ]
    }
  ]
}

```
We are going to load the JSON into our script, and use some nifty DOM manipulation to display it, like this:
<img width="1468" height="885" alt="image" src="https://github.com/user-attachments/assets/47aa0372-aea8-4b92-a691-1c0dadae2592" />

## Top-level function

```js
async function populate() {
  const requestURL =
    "https://mdn.github.io/learning-area/javascript/oojs/json/superheroes.json";
  const request = new Request(requestURL);

  const response = await fetch(request);
  const superHeroes = await response.json();

  populateHeader(superHeroes);
  populateHeroes(superHeroes);
}
```
<p>
To obtain the JSON, we use an API called Fetch. This API allows us to make network requests to retrieve resources from a server via JavaScript (e.g., images, text, JSON, even HTML snippets), meaning that we can update small sections of content without having to reload the entire page.

In our function, the first four lines use the Fetch API to fetch the JSON from the server:

we declare the requestURL variable to store the GitHub URL
we use the URL to initialize a new Request object.
we make the network request using the fetch() function, and this returns a Response object
we retrieve the response as JSON using the json() function of the Response object.
</p>

After all that, the superHeroes variable will contain the JavaScript object based on the JSON. We are then passing that object to two function calls — the first one fills the <header> with the correct data, while the second one creates an information card for each hero on the team, and inserts it into the `<section>.`


## Populating the header

<p>
  Now that we've retrieved the JSON data and converted it into a JavaScript object, let's make use of it by writing the two functions we referenced above. First of all, add the following function definition below the previous code:
</p>

```js
function populateHeader(obj) {
  const header = document.querySelector("header");
  const myH1 = document.createElement("h1");
  myH1.textContent = obj.squadName;
  header.appendChild(myH1);

  const myPara = document.createElement("p");
  myPara.textContent = `Hometown: ${obj.homeTown} // Formed: ${obj.formed}`;
  header.appendChild(myPara);
}
```

## Creating the hero information cards

> Next, add the following function at the bottom of the code, which creates and displays the superhero cards:
>
```js
function populateHeroes(obj) {
  const section = document.querySelector("section");
  const heroes = obj.members;

  for (const hero of heroes) {
    const myArticle = document.createElement("article");
    const myH2 = document.createElement("h2");
    const myPara1 = document.createElement("p");
    const myPara2 = document.createElement("p");
    const myPara3 = document.createElement("p");
    const myList = document.createElement("ul");

    myH2.textContent = hero.name;
    myPara1.textContent = `Secret identity: ${hero.secretIdentity}`;
    myPara2.textContent = `Age: ${hero.age}`;
    myPara3.textContent = "Superpowers:";

    const superPowers = hero.powers;
    for (const power of superPowers) {
      const listItem = document.createElement("li");
      listItem.textContent = power;
      myList.appendChild(listItem);
    }

    myArticle.appendChild(myH2);
    myArticle.appendChild(myPara1);
    myArticle.appendChild(myPara2);
    myArticle.appendChild(myPara3);
    myArticle.appendChild(myList);

    section.appendChild(myArticle);
  }
}
```

>Create several new elements: an <article>, an <h2>, three <p>s, and a <ul>.
>Set the <h2> to contain the current hero's name.
>Fill the three paragraphs with their secretIdentity, age, and a line saying "Superpowers:" to introduce the information in >the list.
>Store the powers property in another new constant called superPowers — this contains an array that lists the current >hero's superpowers.
>Use another for...of loop to loop through the current hero's superpowers — for each one we create an <li> element, put the >superpower inside it, then put the listItem inside the <ul> element (myList) using appendChild().
>The very last thing we do is to append the <h2>, <p>s, and <ul> inside the <article> (myArticle), then append the > `<article>` inside the <section>. The order in which things are appended is important, as this is the order they will be > displayed inside the HTML

## Calling the top-level function

``` populate();```

## Converting between objects and text

> sometimes we aren't so lucky — sometimes we receive a raw JSON string, and we need to convert it to an object ourselves. > And when we want to send a JavaScript object across the network, we need to convert it to JSON (a string) before sending >‌ it. Luckily, these two problems are so common in web development that a built-in JSON object is available in browsers, >‌ which contains the following two methods:

> parse(): Accepts a JSON string as a parameter, and returns the corresponding JavaScript object.
> stringify(): Accepts an object as a parameter, and returns the equivalent JSON string.


<a href="https://github.com/mdn/learning-area/blob/main/javascript/oojs/json/heroes-finished-json-parse.html">source code </a>

```js
async function populate() {
  const requestURL =
    "https://mdn.github.io/learning-area/javascript/oojs/json/superheroes.json";
  const request = new Request(requestURL);

  const response = await fetch(request);
  const superHeroesText = await response.text();

  const superHeroes = JSON.parse(superHeroesText);
  populateHeader(superHeroes);
  populateHeroes(superHeroes);
}
```
Try entering the following lines into your browser's JavaScript console one by one to see it in action:


```
let myObj = { name: "Chris", age: 38 };
myObj;
let myString = JSON.stringify(myObj);
myString;
```
<h2>
<a href="[https://github.com/mdn/learning-area/blob/main/javascript/oojs/json/heroes-finished-json-parse.html](https://developer.mozilla.org/en-US/docs/Learn_web_development/Core/Scripting/Debugging_JavaScript)">
JavaScript debugging and error handling </a>
</h2>


