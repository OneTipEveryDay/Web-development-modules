>Flexbox is a one-dimensional layout method for arranging items in rows or columns. Items flex (expand) to fill additional space or shrink to fit into smaller spaces. <br>
>
>Flexbox features may be the perfect solution for your one dimensional layout needs.
>
# Specifying what elements to lay out as flexible boxes

```html
<header>
  <h1>Sample flexbox example</h1>
</header>
<section>
  <article>
    <h2>First article</h2>
    <p>Content…</p>
  </article>
  <article>
    <h2>Second article</h2>
    <p>Content…</p>
  </article>
  <article>
    <h2>Third article</h2>
    <p>Content…</p>
  </article>
</section>```

```css
body {
  font-family: sans-serif;
  margin: 0;
}
header {
  background: purple;
  height: 100px;
}
h1 {
  text-align: center;
  color: white;
  line-height: 100px;
  margin: 0;
}
section {
  zoom: 0.8;
  display: flex;
}
article {
  padding: 10px;
  margin: 10px;
  background: aqua;
}

```
This causes the <section> element to become a flex container and its children become flex items. <a href="https://developer.mozilla.org/en-US/docs/Learn_web_development/Core/CSS_layout/Flexbox#introducing_a_simple_example">This is what it looks like: </a>

## Columns or rows?


Try adding the following declaration to your <section> rule:

```flex-direction: column;```

You'll see that this puts the items back in a column layout, 

## Wrapping

```
section {
  flex-wrap: wrap;
}
```

> We now have multiple rows. Each row has as many flexbox children fitted into it as is sensible. Any overflow is moved down to the next line.

## Nested flex boxes

<img width="1255" height="521" alt="image" src="https://github.com/user-attachments/assets/a77a6166-a978-467e-a1cf-2546716792e0" />

We've got a <section> element containing three <article>s. The third <article> contains three <div>s, and the first <div> contains five <button>s:

```
section - article
          article
          article - div - button
                    div   button
                    div   button
                          button
                          button
```
<br>

```html
<header>
  <h1>Complex flexbox example</h1>
</header>
<section>
  <article>
    <h2>First article</h2>
    <p>Content…</p>
  </article>
  <article>
    <h2>Second article</h2>
    <p>Content…</p>
  </article>
  <article>
    <div>
      <button>Smile</button>
      <button>Laugh</button>
      <button>Wink</button>
      <button>Shrug</button>
      <button>Blush</button>
    </div>
    <div>
      <p>Paragraph one content…</p>
    </div>
    <div>
      <p>Paragraph two content…</p>
    </div>
  </article>
</section>

```
<br>

```css
body {
  font-family: sans-serif;
  margin: 0;
}
header {
  background: purple;
  height: 100px;
}
h1 {
  text-align: center;
  color: white;
  line-height: 100px;
  margin: 0;
}
article {
  padding: 10px;
  margin: 10px;
  background: aqua;
}
section {
  display: flex;
  zoom: 0.8;
}
article {
  flex: 1 170px;
}
article:nth-of-type(3) {
  flex: 3 170px;
  display: flex;
  flex-flow: column;
}
article:nth-of-type(3) div:first-child {
  flex: 1 100px;
  display: flex;
  flex-flow: row wrap;
  align-items: center;
  justify-content: space-around;
}
button {
  flex: 1 auto;
  margin: 5px;
  font-size: 18px;
  line-height: 1.5;
}

```
 Take special note of the second rule here: we're setting the third <article> to have its children laid out like flex items too, but this time we're laying them out like a column.

```
article {
  flex: 1 100px;
}

article:nth-of-type(3) {
  flex: 3 100px;
  display: flex;
  flex-flow: column;
}
```
Next, we set some flex values on the `<article>` s themselves. Take special note of the second rule here: we're setting the third <article> to have its children laid out like flex items too, but this time we're laying them out like a column.
```
article {
  flex: 1 100px;
}

article:nth-of-type(3) {
  flex: 3 100px;
  display: flex;
  flex-flow: column;
}
```

Next, we select the first <div>. We first use flex: 1 100px; to effectively give it a minimum height of 100px, then we set its children (the <button> elements) to also be laid out like flex items. Here we lay them out in a wrapping row and align them in the center of the available space as we did with the individual button example we saw earlier.

```
article:nth-of-type(3) div:first-child {
  flex: 1 100px;
  display: flex;
  flex-flow: row wrap;
  align-items: center;
  justify-content: space-around;
}
```
## Aligning items in a flex container


























 
