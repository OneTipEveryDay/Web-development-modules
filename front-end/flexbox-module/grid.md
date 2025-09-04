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

```.wrapper {
  display: grid;
}```

<img width="958" height="354" alt="image" src="https://github.com/user-attachments/assets/5de4bacd-c366-40a9-8b90-ad4d788ed457" />
<br>
## Grid tracks

> We define rows and columns on our grid with the `grid-template-rows` and `grid-template-columns` properties. These define grid tracks. A grid track is the space between any two adjacent lines on the grid


## Basic example

> [!IMPORTANT]
> The fr unit <br>
> Tracks can be defined using any length unit. Grid also introduces an additional length unit to help us create flexible grid tracks. The fr unit represents a fraction of the available space in the grid container.

.wrapper {
  display: grid;
  grid-template-columns: 1fr 1fr 1fr;
}


<img width="1421" height="227" alt="image" src="https://github.com/user-attachments/assets/e9d250bb-685a-49db-91da-03643bef46c6" />

## 





























