# bootstrap intro

## Create a new index.html file in your project root
```
<!doctype html>
<html lang="en">

<head>
  <meta charset="utf-8">
  <meta name="viewport" content="width=device-width, initial-scale=1">
  <title>Bootstrap</title>
  <!-- TODO 1: Add the Bootstrap link here. -->
  <style>


  </style>
</head>

<body>
  <div class="flex-container">
    <!-- TODO 2: Add the Bootstrap component here -->

  </div>
</body>


</html>
```

> [!NOTE]
>‌ CDN links
```
<!doctype html>
<html lang="en">
  <head>
    <meta charset="utf-8">
    <meta name="viewport" content="width=device-width, initial-scale=1">
    <title>Bootstrap demo</title>
    <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.8/dist/css/bootstrap.min.css" rel="stylesheet" integrity="sha384-sRIl4kxILFvY47J16cr9ZwB07vP4J8+LH7qKQnuqkuIAvNWLzeN8tE5YBujZqJLB" crossorigin="anonymous">
  </head>
  <body>
    <h1>Hello, world!</h1>
    <script src="https://cdn.jsdelivr.net/npm/bootstrap@5.3.8/dist/js/bootstrap.bundle.min.js" integrity="sha384-FKyoEForCGlyvwx9Hj09JcYn3nv7wiPVlz7YYwJrWVcXK/BmnVDxM+D2scQbITxI" crossorigin="anonymous"></script>
  </body>
</html>
```

> all you need go to <a src"https://getbootstrap.com/docs/5.3/getting-started/introduction/" > documents </a>
> and read `components`
>


to taget a component ceate a `class="flex-container" ` in a div and add some css 
```
  <style>
    .flex-container {
      display: flex;
      height: 100vh;
      justify-content: center;
      align-items: center;
    }
  </style>

<body>
  <div class="flex-container"> </div>
```

 ## bootstrap layout : understanding 12 column bootstrap layout system

<img src="https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcRuYF88lq-D3zQPMKtcICpeP-X65_FVe_FzXwrghVPd_KE49pykoSIB0nbUb49rlF_HJQ&usqp=CAU">

> div class="container"
>   div class="rows"
>     div class="col"
>

<img src="https://designmodo.com/wp-content/uploads/2021/03/1.png">

we write like this:

<img src="https://www.i2tutorials.com/wp-content/media/2020/10/Bootstrap-Grid-System-2.png">

in this example we use `sm` so if client screen small then size sm 'pixel' then any culomn show 100% of screen

### Responsive containers 

Responsive containers allow you to specify a class that is 100% wide until the specified breakpoint is reached, after which we apply max-widths for each of the higher breakpoints. For example, .container-sm is 100% wide to start until the sm breakpoint is reached, where it will scale up with md, lg, xl, and xxl.

```
<div class="container-sm">100% wide until small breakpoint</div>
<div class="container-md">100% wide until medium breakpoint</div>
<div class="container-lg">100% wide until large breakpoint</div>
<div class="container-xl">100% wide until extra large breakpoint</div>
<div class="container-xxl">100% wide until extra extra large breakpoint</div>
```

## Components

### button
<a src="https://getbootstrap.com/docs/5.3/customize/color/"> read more about colors</a>
example:

<img width="1109" height="126" alt="image" src="https://github.com/user-attachments/assets/1b86d472-1125-4850-82a0-96c423795890" />
```
<button type="button" class="btn btn-primary">Primary</button>
<button type="button" class="btn btn-secondary">Secondary</button>
<button type="button" class="btn btn-success">Success</button>
<button type="button" class="btn btn-danger">Danger</button>
<button type="button" class="btn btn-warning">Warning</button>
<button type="button" class="btn btn-info">Info</button>
<button type="button" class="btn btn-light">Light</button>
<button type="button" class="btn btn-dark">Dark</button>
<button type="button" class="btn btn-link">Link</button>
```

Base class <br>
Bootstrap has a base .btn class that sets up basic styles such as padding and content alignment. By default, .btn controls have a transparent border and background color, and lack any explicit focus and hover styles

```html
<button type="button" class="btn">Base class</button>
```

Outline buttons <br>
In need of a button, but not the hefty background colors they bring? Replace the default modifier classes with the .btn-outline-* ones to remove all background images and colors on any button.

<img width="1243" height="107" alt="image" src="https://github.com/user-attachments/assets/fbf82aff-6bbe-49b2-ac83-b9976e16db28" />

```html
<button type="button" class="btn btn-outline-primary">Primary</button>
<button type="button" class="btn btn-outline-secondary">Secondary</button>
<button type="button" class="btn btn-outline-success">Success</button>
<button type="button" class="btn btn-outline-danger">Danger</button>
<button type="button" class="btn btn-outline-warning">Warning</button>
<button type="button" class="btn btn-outline-info">Info</button>
<button type="button" class="btn btn-outline-light">Light wanderful!!!</button>   
<button type="button" class="btn btn-outline-dark">Dark</button>
```

<a src="https://getbootstrap.com/docs/5.3/components/button-group/">Button group
</a>

<a src="https://getbootstrap.com/docs/5.3/components/card/"> cards</a>

> Collapse
<img width="451" height="243" alt="image" src="https://github.com/user-attachments/assets/a697d2de-34d7-40fd-a2cb-6699e13ce5a2" />

```html
<p>
  <button class="btn btn-primary" type="button" data-bs-toggle="collapse" data-bs-target="#collapseWidthExample" aria-expanded="false" aria-controls="collapseWidthExample">
    Toggle width collapse
  </button>
</p>
<div style="min-height: 120px;">
  <div class="collapse collapse-horizontal" id="collapseWidthExample">
    <div class="card card-body" style="width: 300px;">
      This is some placeholder content for a horizontal collapse. It’s hidden by default and shown when triggered.
    </div>
  </div>
</div>
```

>modal js popop 
>Pagination


ش
ش
شش








