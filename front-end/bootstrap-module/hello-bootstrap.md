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

 










