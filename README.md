# css-grid


## The Holy Grail Layout

![holy grail layout]


> A layout so holy,
> [it has its own Wikipedia article](<https://en.wikipedia.org/wiki/Holy_Grail_(web_design)>).

This is something you know well, even if you don't recognize the term. It
describes a webpage with a header, footer, and three columns: a wide "main"
column, a navigation column on the left, and an advertisement, site map, or
extra info column along the right.

Obviously, this layout won't work on tiny screens, unless you really like
super-skinny columns. It's common to stack things on top of each other for
mobile views to make one single column.

Before flexbox or CSS grid, this involved a lot of pushing and shoving with dimensions and
positioning. You would essentially have to write two completely separate
stylesheets (one for mobile, and one for desktop), each to control the different
layours.

With flexbox, just change the `flex-direction` for smaller screen sizes, make
any size / order adjustments on the sections of the page, and you're pretty much
done!

```css
@media screen and (max-width: 600px) {
  main {
    flex-direction: column;
  }

  section {
    order: 1;
  }
}
```


[Example](https://codepen.io/jme11/pen/WNvYQzW)


## Working in CSS Grid

From the [www.w3.org](https://www.w3.org/TR/css-grid-1/) website:

> "Grid Layout is a new layout model for CSS that has powerful abilities to
> control the sizing and positioning of boxes and their contents. Unlike
> Flexible Box Layout, which is single-axis–oriented, Grid Layout is optimized
> for 2-dimensional layouts: those in which alignment of content is desired in
> both dimensions."

With Grid layout, you can divide up the screen into `rows` and `columns` of
sizes of your choosing, and then specify how many rows and columns each `cell`
takes up. Sizing can be fixed, or dynamic, allowing you to create modern
looking, versatile websites.

_Example of **flexbox** layout_

![flex layout example](assets/flex-layout-ex.png)

_example of **grid** layout_

![grid layout example](assets/grid-layout-ex.png)

> Notice that the grid items are aligned (rather than filling up the available
> space) and that cells can take up multiple rows or columns

## You Do: Explore the source code

Let's take a few minutes to
[explore this web app](https://www.inprnt.com/discover/) built with Grid layout.

> This site was built by a former GA student using CSS Grid, Flexbox, and React.

There are a few ways to implement css grid. I'll show you the steps of how I
like to do it.

Feel free to code along in codepen.

1. To start, you must have a _container_ (or _parent_) element, with at least
   one _nested_ (or _child_) elements inside.

```html
<div class="parent">
  <div class="child child-one">1</div>
  <div class="child child-two">2</div>
  <div class="child child-three">3</div>
</div>
```

2. On the container, specify that you are using `display: grid` and what your
   **_template_** will look like - more specifically, your **_rows_** and
   **_columns_**. Here's an example.

```css
.parent {
  display: grid;
  grid-template-rows: 100px 200px 300px;
  grid-template-columns: 100px 1fr 2fr 100px;
}
```

`fr` represents `fraction`, it's a unit that will evenly span the remainder of
the space.

Here we have specified **_3 rows_**, taking up 100, 200, and 300 pixels
respectively. We also specified **_4 columns_**, giving us a total of **_12
cells_**. `grid-template` also takes other units like `%`, `rem`, and `auto`.
For now we will focus on `px` and `fr` units. You can also use `repeat` to
specify multiple rows or columns of one size like this `repeat(5, 1fr)`

3. the _child_ elements, you can specify _where_ the _cells_ are located and the
   _size_ you want them to be. I like to follow this pattern:

```css
selector {
  grid-row: where-to-start / span size;
}
```

> same would work for `grid-column`

So something like this on a _child_ element:

```css
.child-one {
  grid-row: 1 / span 1;
  grid-column: 1 / span 2;
}
```

This element takes up 1 row, starting at row 1, and takes up 2 columns, starting
at column 1.

We could also write `grid-row: 1;` for short, if your element only spans 1 row.

### You do: Griddle me this

Now let's follow along and try to make our _holy grail_ website design using
Grid layout. We will need a header, a footer, two side columns, and a main
section. The starter code has been set up for you
[here](https://codepen.io/perryf/pen/rJNZpw)

Using the grid concepts we just learned, see if you can spend a few minutes
getting the holy grail layout built.

> Try it! Don't read ahead! We'll go over it next.

### We do: Griddle me this 

Now let's add our `grid-template` code to our parent element.

```css
body {
  display: grid;
  grid-template-rows: 80px 1fr 80px;
  grid-template-columns: 100px 1fr 100px;
}
```

Now let's figure out how to format our `header`. We want the header to take up 1
row and 3 columns. Let's give it some color too.

```css
header {
  grid-row: 1;
  grid-column: 1 / span 3;
  background: steelblue;
}
```


Now onto our left column. That will only take up 1 column and one row, starting
at row 2.

```css
.left {
  grid-row: 2;
  grid-column: 1;
  background: lightseagreen;
}
```

The right column can be positioned in a very similar fashion.

```css
.right {
  grid-row: 2;
  grid-column: 3;
  background: mistyrose;
}
```

The main section is the largest section (except on tiny screens) but really only
takes up one row and one column.

```css
main {
  grid-row: 2;
  grid-column: 2;
  background: lemonchiffon;
}
```

Lastly, our footer will take up the entire bottom row, spanning 3 columns.

```css
footer {
  grid-row: 3;
  grid-column: 1 / span 3;
  background: rebeccapurple;
}
```

Solution on [codepen](https://codepen.io/jme11/pen/OJVaywa)


