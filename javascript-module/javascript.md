Let's take a button as an example. We can mark it up using HTML to give it structure and purpose:

```html
<button type="button">Player 1: Chris</button>
```
Then we can add some CSS into the mix to get it looking nice:


```css
button {
  font-family: "helvetica neue", helvetica, sans-serif;
  letter-spacing: 1px;
  text-transform: uppercase;
  border: 2px solid rgb(200 200 0 / 60%);
  background-color: rgb(0 217 217 / 60%);
  color: rgb(100 0 0 / 100%);
  box-shadow: 1px 1px 2px rgb(0 0 200 / 40%);
  border-radius: 10px;
  padding: 3px 10px;
  cursor: pointer;
}
<img width="788" height="274" alt="image" src="https://github.com/user-attachments/assets/584c49c2-305f-4bee-8bab-64a07becf65b" />

```
And finally, we can add some JavaScript to implement dynamic behavior:


```js
function updateName() {
  const name = prompt("Enter a new name");
  button.textContent = `Player 1: ${name}`;
}

const button = document.querySelector("button");

button.addEventListener("click", updateName);
```

> The core client-side JavaScript language consists of some common programming features that allow you to do things like:
>Store useful values inside variables. In the above example for instance, we ask for a new name to be entered then store that name in a variable called name.<br>
> Operations on pieces of text (known as "strings" in programming). In the above example we take the string "Player 1: " and join it to the name variable to create the complete text label, e.g., "Player 1: Chris".<br>
> Running code in response to certain events occurring on a web page. We used a click event in our example above to detect when the label is clicked and then run the code that updates the text label.

In this module we are explicitly talking about client-side JavaScript.
<br>
Server-side code on the other hand is run on the server, then its results are downloaded and displayed in the browser. Examples of popular server-side web languages include PHP, Python, Ruby, C#, and even JavaScript!

##Dynamic versus static code

The word dynamic is used to describe both client-side JavaScript, and server-side languages — it refers to the ability to update the display of a web page/app to show different things in different circumstances, generating new content as required. Server-side code dynamically generates new content on the server, e.g., pulling data from a database, whereas client-side JavaScript dynamically generates new content inside the browser on the client, e.g., creating a new HTML table, filling it with data requested from the server, then displaying the table in a web page shown to the user. The meaning is slightly different in the two contexts, but related, and both approaches (server-side and client-side) usually work together

## Internal JavaScript

1.First : <br>
```
<!DOCTYPE html>
<html lang="en-US">
  <head>
    <meta charset="utf-8">
    <meta name="viewport" content="width=device-width">
    <title>Apply JavaScript example</title>
  </head>
  <body>
    <button>Click me</button>
  </body>
</html>
```
 2.Open the file in your web browser and in your text editor. You'll see that the HTML creates a simple web page containing a clickable button.<br>

 3.Next, go to your text editor and add the following at the bottom of your body — just before your closing `</body>` tag:<br>

```
<script>
  // JavaScript goes here
</script>
```
4.Now we'll add some JavaScript inside our `<script>` element to make the page do something more interesting 

```js
// Function: creates a new paragraph and appends it to the bottom of the HTML body.

function createParagraph() {
  const para = document.createElement("p");
  para.textContent = "You clicked the button!";
  document.body.appendChild(para);
}

/*
  1. Get references to all the buttons on the page in an array format.
  2. Loop through all the buttons and add a click event listener to each one.

  When any button is pressed, the createParagraph() function will be run.
*/

const buttons = document.querySelectorAll("button");

for (const button of buttons) {
  button.addEventListener("click", createParagraph);
}
```


## External JavaScript

1.First, create a new file in the same directory as your sample HTML file. Call it script.js — make sure it has that .js filename extension, as that's how it is recognized as JavaScript.<br>

2.Remove your current <script> element at the bottom of the </body> and add the following just before the closing </head> tag (that way the browser can start loading the file sooner than when it's at the bottom):
```html
<script type="module" src="script.js"></script>
```
3.Inside script.js, add the following script:
```js
function createParagraph() {
  const para = document.createElement("p");
  para.textContent = "You clicked the button!";
  document.body.appendChild(para);
}

const buttons = document.querySelectorAll("button");

for (const button of buttons) {
  button.addEventListener("click", createParagraph);
}
```


## Text strings

```js
function checkGuess() {
  console.log("I am a placeholder");
}
```
<br>


const name = "Mahalia";

const greeting = `Hello ${name}`;

## Conditionals

if (inout === Condition) {
  //do somthing
  }

## loops

const fruits = ["apples", "bananas", "cherries"];
for (const fruit of fruits) {
  console.log(fruit);
}

```js
const resetParas = document.querySelectorAll(".resultParas p");
for (const resetPara of resetParas) {
  resetPara.textContent = "";
}
```
This code creates a variable containing a list of all the paragraphs inside <div class="resultParas"> using the querySelectorAll() method, then it loops through each one, removing the text content of each.

## Variables

Variable example:

```html
<button id="button_A">Press me</button>
<h3 id="heading_A"></h3>
```
```js
const buttonA = document.querySelector("#button_A");
const headingA = document.querySelector("#heading_A");

let count = 1;

buttonA.onclick = () => {
  buttonA.textContent = "Try again!";
  headingA.textContent = `${count} clicks so far`;
  count += 1;
};
```

<img width="1496" height="177" alt="image" src="https://github.com/user-attachments/assets/57d8ba40-2849-4ce9-a4f0-1ac148ba1f37" />

## Declaring a variable

To use a variable, you've first got to create it — more accurately, we call this declaring the variable. To do this, we type the keyword let followed by the name you want to call your variable:

```js
let myName;
let myAge;
```

## Arrays
```
let myNameArray = ["Chris", "Bob", "Jim"]; <br>
let myNumberArray = [10, 15, 40]; <br>

myNameArray[0]; // should return 'Chris'
```

##‌ Objects

```
let dog = { name: "Spot", breed: "Dalmatian" };
```
dog.name;

## Introduction to events

> To react to an event, you attach an event listener to it. This is a code feature that listens out for the event firing. When the event fires, an event handler function (referenced by, or contained inside the event listener) is called to respond to the event firing. When such a block of code is set up to run in response to an event, we say we are registering an event handler.

In the following example, we have a single <button> in the page:


```
<button>Change color</button>
```
```js
const btn = document.querySelector("button");

function random(number) {
  return Math.floor(Math.random() * (number + 1));
}

btn.addEventListener("click", () => {
  const rndCol = `rgb(${random(255)} ${random(255)} ${random(255)})`;
  document.body.style.backgroundColor = rndCol;
});
```
<img width="1376" height="421" alt="image" src="https://github.com/user-attachments/assets/76c3e34d-f34e-4b4d-85f7-988de4a4bb63" />

## Adding multiple listeners for a single event

```js
myElement.addEventListener("click", functionA);
myElement.addEventListener("click", functionB);
```

Both functions would now run when the element is clicked.

## Extra properties of event objects
> Some event objects add extra properties that are relevant to that particular type of event. For example, the keydown event fires when the user presses a key. Its event object is a KeyboardEvent, which is a specialized Event object with a key property that tells you which key was pressed:
> 
>
```
<input id="textBox" type="text" />
<div id="output"></div>
```
```js
const textBox = document.querySelector("#textBox");
const output = document.querySelector("#output");
textBox.addEventListener("keydown", (event) => {
  output.textContent = `You pressed "${event.key}".`;
});
```

<img width="1391" height="223" alt="image" src="https://github.com/user-attachments/assets/45f2f418-9e55-4485-a823-d7111e2ba700" />

## Event bubbling

In this chapter we'll look at event bubbling — this is what happens when you add an event listener to a parent element, and the user clicks the child element.

```html
<div id="container">
  <button>Click me!</button>
</div>
<pre id="output"></pre>
```

```js
const output = document.querySelector("#output");
function handleClick(e) {
  output.textContent += `You clicked on a ${e.currentTarget.tagName} element\n`;
}

const container = document.querySelector("#container");
const button = document.querySelector("button");

document.body.addEventListener("click", handleClick);
container.addEventListener("click", handleClick);
button.addEventListener("click", handleClick);
```

<img width="952" height="188" alt="image" src="https://github.com/user-attachments/assets/c8c63d27-9d95-486e-9992-8332117ecaad" />

>In this case:
> <ul>
> <li>the click on the button fires first. </li>
>‌ <li>followed by the click on its parent (the <div> element).</li>
> <li>followed by the click on the <div> element's parent (the <body> element </li>
> </ul>

We describe this by saying that the event bubbles up from the innermost element that was clicked.



## DOM (Document Object Model) scripting introduction
We have created an example page

```html
<!doctype html>
<html lang="en-US">
  <head>
    <meta charset="utf-8" />
    <title>Simple DOM example</title>
  </head>
  <body>
    <section>
      <img
        src="dinosaur.png"
        alt="A red Tyrannosaurus Rex: A two legged dinosaur
        standing upright like a human, with small arms, and a
        large head with lots of sharp teeth." />
      <p>
        Here we will add a link to the
        <a href="https://www.mozilla.org/">Mozilla homepage</a>
      </p>
    </section>
  </body>
</html>
```

The DOM on the other hand looks like this:


<img width="1440" height="802" alt="image" src="https://github.com/user-attachments/assets/d43f0fdd-4444-4b92-a8ee-ae6ae29af355" />
Each entry in the tree is called a node. 

> Root node: The top node in the tree, which in the case of HTML is always the HTML node (other markup vocabularies like SVG and custom XML will have different root elements).
> Child node: A node directly inside another node. For example, IMG is a child of SECTION in the above example.
> Descendant node: A node anywhere inside another node. For example, IMG is a child of SECTION in the above example, and it is also a descendant. IMG is not a child of BODY, as it is two levels below it in the tree, but it is a descendant of BODY.
> Parent node: A node which has another node inside it. For example, BODY is the parent node of SECTION in the above example.
> Sibling nodes: Nodes that sit on the same level under the same parent node in the DOM tree. For example, IMG and P are siblings in the above example.

## Doing some basic DOM manipulation

Add a <script></script> element just above the closing </body> tag (top html code)
<br>
To manipulate an element inside the DOM, you first need to select it and store a reference to it inside a variable. Inside your script element, add the following line:
```const link = document.querySelector("a");```

Now we have the element reference stored in a variable, we can start to manipulate it using properties and methods available to it (these are defined on interfaces like HTMLAnchorElement in the case of <a> element, its more general parent interface HTMLElement, and Node — which represents all nodes in a DOM). First of all, let's change the text inside the link by updating the value of the Node.textContent property. Add the following line below the previous one:

```link.textContent = "Mozilla Developer Network";
link.href = "https://developer.mozilla.org";
```

## Creating and placing new nodes
...

## Moving and removing elements

...















