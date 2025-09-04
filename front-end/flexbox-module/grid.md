# Grid container

In this example, we have a containing div with a class of wrapper. Nested inside are five child elements.

```html
<div class="wrapper">
  <div>One</div>
  <div>Two</div>
  <div>Three</div>
  <div>Four</div>
  <div>Five</div>
</div>
```
We make the .wrapper a grid container using `display: grid;`.

```
.wrapper {
  display: grid;
}
```

<img width="958" height="354" alt="image" src="https://github.com/user-attachments/assets/5de4bacd-c366-40a9-8b90-ad4d788ed457" />
<br>
## Grid tracks

> We define rows and columns on our grid with the `grid-template-rows` and `grid-template-columns` properties. These define grid tracks. A grid track is the space between any two adjacent lines on the grid

## Basic example

> [!IMPORTANT]
> The fr unit <br>
> Tracks can be defined using any length unit. Grid also introduces an additional length unit to help us create flexible grid tracks. The fr unit represents a fraction of the available space in the grid container.
```
.wrapper {
  display: grid;
  grid-template-columns: 1fr 1fr 1fr;
}
```

<img width="1421" height="227" alt="image" src="https://github.com/user-attachments/assets/e9d250bb-685a-49db-91da-03643bef46c6" />

## Grid lines
It should be noted that when we define a grid we define the grid tracks, not the lines. Grid then gives us numbered lines to use when positioning items. In our three column, two row grid we have four column lines.

<img width="1430" height="827" alt="image" src="https://github.com/user-attachments/assets/a0c706c2-ee66-4188-b98c-06003a45365c" />

## Positioning items against lines

In this example, the first two items on our three column track grid are placed using the grid-column-start, grid-column-end, grid-row-start and grid-row-end properties. Working from left to right, the first item is placed against column line 1, and spans to column line 4, which in our case is the far-right line on the grid. It begins at row line 1 and ends at row line 3, therefore spanning two row tracks.

```
<div class="wrapper">
  <div class="box1">One</div>
  <div class="box2">Two</div>
  <div class="box3">Three</div>
  <div class="box4">Four</div>
  <div class="box5">Five</div>
</div>
```

```CSS
.wrapper {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  grid-auto-rows: 100px;
}

.box1 {
  grid-column-start: 1;
  grid-column-end: 4;
  grid-row-start: 1;
  grid-row-end: 3;
}

.box2 {
  grid-column-start: 1;
  grid-row-start: 3;
  grid-row-end: 5;
}
```
or 
```CSS
.wrapper {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  grid-auto-rows: 100px;
}

.box1 {
  grid-column: 1 / 4;
  grid-row: 1 / 3;
}

.box2 {
  grid-column: 1;
  grid-row: 3 / 5;
}
```


<img width="1431" height="814" alt="image" src="https://github.com/user-attachments/assets/a54c874c-5bd4-4bf7-b873-ef99da76bf0f" />


## Nesting grids

<img width="1491" height="855" alt="image" src="https://github.com/user-attachments/assets/605523c6-6b8b-4328-9bde-052c2d1b8463" />

```
.box1 {
  grid-column-start: 1;
  grid-column-end: 4;
  grid-row-start: 1;
  grid-row-end: 3;
  display: grid;
  grid-template-columns: repeat(3, 1fr);
}
```

```html
<div class="wrapper">
  <div class="box box1">
    <div class="nested">a</div>
    <div class="nested">b</div>
    <div class="nested">c</div>
  </div>
  <div class="box box2">Two</div>
  <div class="box box3">Three</div>
  <div class="box box4">Four</div>
  <div class="box box5">Five</div>
</div>
```
```CSS
* {
  box-sizing: border-box;
}

.wrapper {
  border: 2px solid #f76707;
  border-radius: 5px;
  gap: 3px;
  background-color: #fff4e6;
  display: grid;
  grid-template-columns: repeat(3, 1fr);
}

.box {
  border: 2px solid #ffa94d;
  border-radius: 5px;
  background-color: #ffd8a8;
  padding: 1em;
  color: #d9480f;
}

.box1 {
  grid-column: 1 / 4;
}

.nested {
  border: 2px solid #ffec99;
  border-radius: 5px;
  background-color: #fff9db;
  padding: 1em;
}


```


<img width="1472" height="422" alt="image" src="https://github.com/user-attachments/assets/aebdafc8-a8c9-4392-9a93-4d7a109aba06" />



## <a href="https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_grid_layout/Relationship_of_grid_layout_with_other_layout_methods">Relationship of grid layout to other layout methods</a>




















