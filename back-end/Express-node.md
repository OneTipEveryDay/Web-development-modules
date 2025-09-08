# Express/Node introduction

>Node (or more formally Node.js) is an open-source, cross-platform runtime environment that allows developers to create all kinds of server-side tools and applications in JavaScript. The runtime is intended for use outside of a browser context (i.e., running directly on a computer or server OS). As such, the environment omits browser-specific JavaScript APIs and adds support for more traditional OS APIs including HTTP and file system libraries


## File system

> The `node:fs`  module enables interacting with the file system in a way modeled on standard POSIX functions.allow us to acsses to local storege
>  <br> next import neded module
> then you can search in nodejs.org to find methode

```
import * as fs from 'node:fs';

fs.radFile(path[,option],callback);

```


## NPM
> to ceate `package.json` in terminal write
``` npm init```
> now you can install packages from npmjs.com
``` npm i <something> ```
> see documents to how use package . when save methode(come from package in a var ) flash back to preveosle module


## Helloworld Express

ceate app.js :
```js
const express = require("express");

const app = express();
const port = 3000;

app.get("/", (req, res) => {
  res.send("Hello World!");
});

app.listen(port, () => {
  console.log(`Example app listening on port ${port}!`);
});
```

The first two lines require() (import) the express module and create an Express application. This object, which is traditionally named app, has methods for routing HTTP requests,

> [!IMPORTANT]
> The middle part of the code (the three lines starting with app.get) shows a route definition. The app.get() method specifies a callback function that will be invoked whenever there is an HTTP GET request with a path ('/') relative to the site root. The callback function takes a request and a response object as arguments, and calls send() on the response to return the string "Hello World!"
> 


## Importing and creating modules
> A module is a JavaScript library/file that you can import into other code using Node's require() function. Express itself is a module, as are the middleware and database libraries that we use in our Express applications.
```
const express = require("express");

const app = express();

```

## Using asynchronous APIs

JavaScript code frequently uses asynchronous rather than synchronous APIs for operations that may take some time to complete. A synchronous API is one in which each operation must complete before the next operation can start.
for example:
```
console.log("First");
console.log("Second");
```

> By contrast, an asynchronous API is one in which the API will start an operation and immediately return (before the operation is complete). Once the operation finishes, the API will use some mechanism to perform additional operations
 ```
 setTimeout(() => {
  console.log("First");
}, 3000);
console.log("Second");
```
## Creating route handlers
In our Hello World Express example (see above), we defined a (callback) route handler function for HTTP GET requests to the site root ('/').

<br>
The callback function takes a request and a response object as arguments. In this case, the method calls send() on the response to return the string "Hello World!" 

> There is a special routing method, app.all(), which will be called in response to any HTTP method. This is used for loading middleware functions at a particular path for all request methods. The following example (from the Express documentation) shows a handler that will be executed for requests to /secret irrespective of the HTTP verb used (provided it is supported by the http module).
```js
app.all("/secret", (req, res, next) => {
  console.log("Accessing the secret section…");
  next(); // pass control to the next handler
});
```
Often it is useful to group route handlers for a particular part of a site together and access them using a common route-prefix
> For example, we can create our wiki route in a module named wiki.js, and then export the Router object, as shown below:
```js
// wiki.js - Wiki route module

const express = require("express");

const router = express.Router();

// Home page route
router.get("/", (req, res) => {
  res.send("Wiki home page");
});

// About page route
router.get("/about", (req, res) => {
  res.send("About this wiki");
});

module.exports = router;
```
## Using middleware

> Middleware is used extensively in Express apps, for tasks from serving static files to error handling, to compressing HTTP responses. Whereas route functions end the HTTP request-response cycle by returning some response to the HTTP client, middleware functions typically perform some operation on the request or response and then call the next function in the "stack", which might be more middleware or a route handler. The order in which middleware is called is up to the app developer.
> <br>
>Most apps will use third-party middleware in order to simplify common web development tasks like working with cookies, sessions, user authentication, accessing request POST and JSON data, logging, etc
> To use third party middleware you first need to install it into your app using npm. For example, to install the morgan HTTP request logger middleware, you'd do this:
>  
```bash
npm install morgan
```
You could then call use() on the Express application object to add the middleware to the stack:


```js
const express = require("express");
const logger = require("morgan");

const app = express();
app.use(logger("dev"));
// …
```
The example below shows how you can add the middleware function using both approaches, and with/without a route.

```js
const express = require("express");

const app = express();

// An example middleware function
function middlewareFunction(req, res, next) {
  // Perform some operations
  next(); // Call next() so Express will call the next middleware function in the chain.
}

// Function added with use() for all routes and verbs
app.use(middlewareFunction);

// Function added with use() for a specific route
app.use("/some-route", middlewareFunction);

// A middleware function added for a specific HTTP verb and route
app.get("/", middlewareFunction);

app.listen(3000);
```

## Serving static files

You can use the express.static middleware to serve static files, including your images, CSS and JavaScript (static() is the only middleware function that is actually part of Express). For example, you would use the line below to serve images, CSS files, and JavaScript files from a directory named 'public' at the same level as where you call node:

```app.use(express.static("public"));```

Any files in the public directory are served by adding their filename (relative to the base "public" directory) to the base URL. So for example:

`http://localhost:3000/images/dog.jpg <br>
http://localhost:3000/css/style.css <br>
http://localhost:3000/js/app.js <br>
http://localhost:3000/about.html`

You can also create a virtual prefix for your static URLs, rather than having the files added to the base URL. For example, here we specify a mount path so that the files are loaded with the prefix "/media":

``` app.use("/media", express.static("public"));```

`http://localhost:3000/media/images/dog.jpg <br>
http://localhost:3000/media/video/cat.mp4 <br>
http://localhost:3000/media/cry.mp3` 

## Using databases
In order to use these you have to first install the database driver using npm. For example, to install the driver for the popular NoSQL MongoDB you would use the command:

```b npm install mongodb```

```js
const { MongoClient } = require("mongodb");

MongoClient.connect("mongodb://localhost:27017/animals", (err, client) => {
  if (err) throw err;

  const db = client.db("animals");
  db.collection("mammals")
    .find()
    .toArray((err, result) => {
      if (err) throw err;
      console.log(result);
      client.close();
    });
});
```

#  Creating a skeleton website

## Using the application generator

```BASH
npm install express-generator -g
```
> The Express Application Generator allows you to configure a number of popular view/templating engines, including EJS, Hbs, Pug (Jade), Twig, and Vash
> Generally speaking, you should select a templating engine that delivers all the functionality you need and allows you to be productive sooner
> he Express Application Generator allows you to create a project that is configured to use the most common CSS stylesheet engines: LESS, SASS, Stylus.
> 

## Creating the project

For the sample Local Library app we're going to build, we'll create a project named express-locallibrary-tutorial using the Pug template library and no CSS engine.

> First, navigate to where you want to create the project and then run the Express Application Generator in the command prompt as shown:

```BASH
express express-locallibrary-tutorial --view=pug
```

> At the end of the output, the generator provides instructions on how to install the dependencies (as listed in the package.json file) and how to run the application on different operating systems.
>  At the end of the output, the generator provides instructions on how to install the dependencies (as listed in the package.json file) and how to run the application on different operating systems.
>
```
    change directory:
     $ cd express-locallibrary-tutorial

   install dependencies:
     $ npm install

   run the app:
     $ DEBUG=express-locallibrary-tutorial:* npm start
```
<img width="615" height="338" alt="image" src="https://github.com/user-attachments/assets/711a3780-0890-4762-a794-5f15d0753cd3" />

Congratulations! You now have a working Express application that can be accessed via port 3000.

## Routes and controllers


















