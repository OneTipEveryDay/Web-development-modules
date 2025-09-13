what is react ?‌ ` a javascript library for building user interface همچنین یک صفحه رابط کاربری \یچیده را به اجزای یا کامپوننت های مجزا به صورت درخت مجزا میکنه`
<br>
> perevicely we try to expret html , css , js but tract compunent combine them and bild a module . so for write clean code project help you
> in react louded compunent1 , 2 ,3, 4 ,... so desent need to loud all of a jayen page in secend . useful in twiter page ...
> scale website easy
> rerender efeshently

### CodeSandBox.com

> 1. create a project
> 2. you see a skelete a project : index.js , public ,...
> 3. entry point is public/index.html to `script index.js ` and we dont write code here but write a `<div id=rooot> `
> 4. create index.js
> 5. add dependese (react)
> 6. `import react from "react";        import { createRoot } from "react-dom/client";`
> 7. `const root = createRoot(document.getElementById("app"));    root.render(<h1>helooo</h1>);`

> 9. react work with JSX file format and Babel is a javascript compiler
 
 for build a skelet run ```npm create vite@latest PROJECTNAME --template react ```
<br>
 for Start the development server: `npm run dev`

###  javascript code inside html code inside index.js

>‌ if we have varible that i want to show in h1 taq inside index.js how can i do?

```
import "./styles.css";
import React from "react";
import { createRoot } from "react-dom/client";

var name = "momahdi";

const root = createRoot(document.getElementById("app"));

root.render(<h1>hello {name}</h1>);

```
even you can write javascript code inside {} 

```
import "./styles.css";
import React from "react";
import { createRoot } from "react-dom/client";

var name = "momahdi";

const root = createRoot(document.getElementById("app"));

root.render(<h1>hello { Math.random() }</h1>);

```
we cont write javascript statment! like

```
{
 if (name == moamahdi){
  //do somthing}
 else{
  //de somthing else}

}
```
(what is deffrence expresion and statment ? )


## how to add css (styling)?
> 1. target a eleman and create a className atrebute
> 2. open style.css and write your code in `.className {//somthing}

contenteditable

```
<h1 className="atrib" contenteditable="true">
    hello {name}
  </h1>
```
# React component 
we want create a function  return a html element (h1)

> 1.create a function :
```
function Heading() {
 return <h1> hello world </h1>
}
```
> 2. write `<Heading/>` evrywere you want to show h1
> 3. create a file Heading.jsx and function Heading()  Ctrl+X Ctrl+V here
> 4. beffore it you must import react from "React";
> 5. then

```
export default Heading;
```

> 7.back to index.js and import Hrading from "./Heading";
> 8. end
>

# React Props

> sopose we have pictures + `<p>`s (many div) for using react we Write a function that have component (img h1 p)
> but we have problem
> for calling  them we dont have costomiz atrebute for objects
> you must bellow on object write `<input >` tag then you can write `<objecName   costomizeAtrebute = value />`
> now function(props) {};
> you can use props.costomizeAtrebute then see value

example code: 

<img width="994" height="314" alt="image" src="https://github.com/user-attachments/assets/84596f63-ed21-4b9e-8649-54ad1b18b764" />

vite-config.js

```
import { defineConfig } from 'vite'
import react from '@vitejs/plugin-react'

// https://vitejs.dev/config/
export default defineConfig({
  plugins: [react()],
})
```
app.jsx

```
import React from "react";
import Card from "./Card";
import contacts from "../contacts";

function App() {
  return (
    <div>
      <h1 className="heading">My Contacts</h1>
      <Card
        name={contacts[0].name}
        img={contacts[0].imgURL}
        tel={contacts[0].phone}
        email={contacts[0].email}
      />
      <Card
        name={contacts[1].name}
        img={contacts[1].imgURL}
        tel={contacts[1].phone}
        email={contacts[1].email}
      />
      <Card
        name={contacts[2].name}
        img={contacts[2].imgURL}
        tel={contacts[2].phone}
        email={contacts[2].email}
      />
    </div>
  );
}

export default App;

```
contacts.js
```
const contacts = [
  {
    name: "Beyonce",
    imgURL:
      "https://blackhistorywall.files.wordpress.com/2010/02/picture-device-independent-bitmap-119.jpg",
    phone: "+123 456 789",
    email: "b@beyonce.com"
  },
  {
    name: "Jack Bauer",
    imgURL:
      "https://pbs.twimg.com/profile_images/625247595825246208/X3XLea04_400x400.jpg",
    phone: "+987 654 321",
    email: "jack@nowhere.com"
  },
  {
    name: "Chuck Norris",
    imgURL:
      "https://i.pinimg.com/originals/e3/94/47/e39447de921955826b1e498ccf9a39af.png",
    phone: "+918 372 574",
    email: "gmail@chucknorris.com"
  }
];

export default contacts;

```



















