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

In <a href="https://github.com/OneTipEveryDay/Web-development-modules/new/main/back-end"> Using a Database (with Mongoose) </a> we defined Mongoose models to interact with the database, and used a (standalone) script to create some initial library records. We can now write the code to present that information to users.

> The diagram below is provided as a reminder of the main flow of data and things that need to be implemented when handling an HTTP request/response. In addition to the views and routes the diagram shows "controllers" — functions that separate out the code to route requests from the code that actually processes requests.
As we've already created the models, the main things we'll need to create are:

<ul>
  <li>"Routes" to forward the supported requests (and any information encoded in request URLs) to the appropriate controller functions.</li>
  <li>
Controller functions to get the requested data from the models, create an HTML page displaying the data, and return it to the user to view in the browser.</li>
  <li>
Views (templates) used by the controllers to render the data.
</li>
</ul>

## Routes primer

> A route is a section of Express code that associates an HTTP verb (GET, POST, PUT, DELETE, etc.), a URL path/pattern, and a function that is called to handle that pattern.

## Defining and using separate route modules

The code below provides a concrete example of how we can create a route module and then use it in an Express application.
```js
// wiki.js - Wiki route module.

const express = require("express");

const router = express.Router();

// Home page route.
router.get("/", (req, res) => {
  res.send("Wiki home page");
});

// About page route.
router.get("/about", (req, res) => {
  res.send("About this wiki");
});

module.exports = router;
```
> To use the router module in our main app file we first require() the route module (wiki.js). We then call use() on the > Express application to add the Router to the middleware handling path, specifying a URL path of 'wiki'.

```
const wiki = require("./wiki.js");

// …
app.use("/wiki", wiki);
```

The two routes defined in our wiki route module are then accessible from /wiki/ and /wiki/about/.

## Route functions

> The callback takes three arguments (usually named as shown: req, res, next), that will contain the HTTP Request object, > HTTP response, and the next function in the middleware chain
> The callback function here calls send() on the response to return the string "About this wiki" when we receive a GET > request with the path (/about). 
>  you could call res.json() to send a JSON response or res.sendFile() to send a file. The response method that we'll be using most often as we build up the library is render(), which creates and returns HTML files using templates and data—we'll talk a lot more about that in a later article!

## Create the catalog route module

Next we create routes for all the URLs needed by the LocalLibrary website, which will call the controller functions we defined in the previous sections.

```
/express-locallibrary-tutorial # the project root
  /routes
    index.js
    users.js
    catalog.js
```
Open /routes/catalog.js and copy in the code below:

```js

const express = require("express");

// Require controller modules.
const book_controller = require("../controllers/bookController");
const author_controller = require("../controllers/authorController");
const genre_controller = require("../controllers/genreController");
const book_instance_controller = require("../controllers/bookinstanceController");

const router = express.Router();

/// BOOK ROUTES ///

// GET catalog home page.
router.get("/", book_controller.index);

// GET request for creating a Book. NOTE This must come before routes that display Book (uses id).
router.get("/book/create", book_controller.book_create_get);

// POST request for creating Book.
router.post("/book/create", book_controller.book_create_post);

// GET request to delete Book.
router.get("/book/:id/delete", book_controller.book_delete_get);

// POST request to delete Book.
router.post("/book/:id/delete", book_controller.book_delete_post);

// GET request to update Book.
router.get("/book/:id/update", book_controller.book_update_get);

// POST request to update Book.
router.post("/book/:id/update", book_controller.book_update_post);

// GET request for one Book.
router.get("/book/:id", book_controller.book_detail);

// GET request for list of all Book items.
router.get("/books", book_controller.book_list);

/// AUTHOR ROUTES ///

// GET request for creating Author. NOTE This must come before route for id (i.e. display author).
router.get("/author/create", author_controller.author_create_get);

// POST request for creating Author.
router.post("/author/create", author_controller.author_create_post);

// GET request to delete Author.
router.get("/author/:id/delete", author_controller.author_delete_get);

// POST request to delete Author.
router.post("/author/:id/delete", author_controller.author_delete_post);

// GET request to update Author.
router.get("/author/:id/update", author_controller.author_update_get);

// POST request to update Author.
router.post("/author/:id/update", author_controller.author_update_post);

// GET request for one Author.
router.get("/author/:id", author_controller.author_detail);

// GET request for list of all Authors.
router.get("/authors", author_controller.author_list);

/// GENRE ROUTES ///

// GET request for creating a Genre. NOTE This must come before route that displays Genre (uses id).
router.get("/genre/create", genre_controller.genre_create_get);

// POST request for creating Genre.
router.post("/genre/create", genre_controller.genre_create_post);

// GET request to delete Genre.
router.get("/genre/:id/delete", genre_controller.genre_delete_get);

// POST request to delete Genre.
router.post("/genre/:id/delete", genre_controller.genre_delete_post);

// GET request to update Genre.
router.get("/genre/:id/update", genre_controller.genre_update_get);

// POST request to update Genre.
router.post("/genre/:id/update", genre_controller.genre_update_post);

// GET request for one Genre.
router.get("/genre/:id", genre_controller.genre_detail);

// GET request for list of all Genre.
router.get("/genres", genre_controller.genre_list);

/// BOOKINSTANCE ROUTES ///

// GET request for creating a BookInstance. NOTE This must come before route that displays BookInstance (uses id).
router.get(
  "/bookinstance/create",
  book_instance_controller.bookinstance_create_get,
);

// POST request for creating BookInstance.
router.post(
  "/bookinstance/create",
  book_instance_controller.bookinstance_create_post,
);

// GET request to delete BookInstance.
router.get(
  "/bookinstance/:id/delete",
  book_instance_controller.bookinstance_delete_get,
);

// POST request to delete BookInstance.
router.post(
  "/bookinstance/:id/delete",
  book_instance_controller.bookinstance_delete_post,
);

// GET request to update BookInstance.
router.get(
  "/bookinstance/:id/update",
  book_instance_controller.bookinstance_update_get,
);

// POST request to update BookInstance.
router.post(
  "/bookinstance/:id/update",
  book_instance_controller.bookinstance_update_post,
);

// GET request for one BookInstance.
router.get("/bookinstance/:id", book_instance_controller.bookinstance_detail);

// GET request for list of all BookInstance.
router.get("/bookinstances", book_instance_controller.bookinstance_list);

module.exports = router;
```

## Update the index route module

We've set up all our new routes, but we still have a route to the original page. Let's instead redirect this to the new index page that we've created at the path /catalog.
<br>
Open /routes/index.js and replace the existing route with the function below.

```
// GET home page.
router.get("/", (req, res) => {
  res.redirect("/catalog");
});
```
## Update app.js
Open app.js and require the catalog route below the other routes (add the third line shown below, underneath the other two that should be already present in the file):
```
const indexRouter = require("./routes/index");
const usersRouter = require("./routes/users");
const catalogRouter = require("./routes/catalog"); // Import routes for "catalog" area of site
```

Next, add the catalog route to the middleware stack below the other routes (add the third line shown below, underneath the other two that should be already present in the file):
```
app.use("/", indexRouter);
app.use("/users", usersRouter);
app.use("/catalog", catalogRouter); // Add catalog routes to middleware chain.
```
## Testing the routes

```$
DEBUG=express-locallibrary-tutorial:* npm start
```


# Displaying library data

>‌ We're now ready to add the pages that display the LocalLibrary website books and other data
>In our previous tutorial articles, we defined Mongoose models that we can use to interact with a database and created some initial library records. We then created all the routes needed for the LocalLibrary website
>The next step is to provide proper implementations for the pages that display our library information (we'll look at implementing pages featuring forms to create, update, or delete information in later articles). This includes updating the controller functions to fetch records using our models and defining templates to display this information to users.


# resourse for myself



















































