# CSS Grid Essentials

## Problem Statement

There are various ways to build a responsive website layout. Choosing one can be
confusing and implementing it can be complicated. The best solution is one that
is quick, structured and comprehensive. Enter CSS Grid.

## Objectives

1.  Create a CSS Grid layout
2.  Identify CSS Grid properties

## Create a CSS Grid Layout

CSS Grid is a set of properties that allow us to rapidly build responsive
layouts for websites. Similar to flexbox, you can use grid properties to build
parts of an HTML page that grow and shrink dynamically, looking good on a
variety of screen sizes.

However, where flexbox gives you very granular control over how individual
elements stretch, shrink and behave in a flex container, grid places a greater
emphasis on setting up the rules of the container itself, automatically handling
the stretching and shrinking of elements by aligning them to rows and columns.
Grid is designed for displaying content in two directions, whereas flexbox is
designed for displaying in one direction.

We're going to dive straight in and set up a grid, then discuss the
properties involved. We're starting out with some basic code in our `index.html`
and `index.css` files. Open up the `index.html` in a browser tab, or if you're
using the Learn IDE, run `httpserver` and navigate to the IP address provided.
Currently, in our HTML, we have one div with a class `grid-container`, and
twelve divs inside of it.

If we look at the page in our browser, it is displaying the twelve divs,
stacked and filling the width of the screen. To turn this into a grid, we
need to apply some properties to the `grid-container` class in our `index.css`
file. First, add the property `display`, and set it to `grid`. Save and
refresh `index.html` in browser. Now, our twelve divs fill the page, evenly
dividing the height of our window. So, we see that using `display: grid`
alone takes all of an element's immediate children and evenly spaces them out,
effectively treating each div as a _row_ in one _column_.

To give this grid a second dimension, we just need to add one property. Just
below `display: grid` in the `grid-container` class, add in:

```
grid-template: 1fr 1fr 1fr 1fr / 1fr 1fr 1fr;
```

Save and take a look at our page now. Instead of a just stack of twelve divs,
we now have a working grid! How is this working? In our `grid-template`
property, we're using a unique _fraction_ unit, `fr`, with a total of four
fractions, representing the number of rows in our grid, and then three more
fractions, representing the number of columns. We can set these to whatever we
would like. Let's swap them to see what happens: remove one `1fr` from the
first set and move it to the second. Now, our page is displaying three rows
and four columns!

In both examples, although we altered the grid structure, the divs inside
automatically arranged to fit while remaining in order. They currently take up
the whole page because both of these example grids have exactly twelve cells.

If you add extra fractions, say five `1fr` units for both rows and columns, the
twelve divs will be arranged into the first twelve available cells, leaving the
rest of the grid empty. If we do the opposite and remove our fraction units
until there are less than twelve cells defined in `grid-template`, the
remaining divs will still be displayed within the grid, but will be appended
to the bottom.

We can also define some rows or columns as bigger than others. In
`grid-template`, you can test this out by changing any of the `1fr` units to
`2fr`. Now, the corresponding row or column will be twice as large as the
others.

Grids are often used to display an indeterminate amount of content - for
example, available products or a list of movies. In order to do this, when we
define the number of columns or rows in our `grid-template`, we can assign
`auto`. Set `grid-template` to `auto / 1fr 1fr 1fr`, save and check out the
page again.

This time, we're back to our original grid. However, we've defined the three
columns, but have now set it so the browser decides how many rows are
necessary. If you set just two columns, we will end up with six rows. Setting
five columns will produce three rows, with three empty cells at the end.

## Identify CSS Grid Properties

Before we do anything else to our grid, let's talk about the specific properties CSS
Grid provides.

#### `display: grid`

Any time we want to implement a CSS grid, we must define it within the
`display` property of the parent element. This causes the browser to interpret
all child elements of the parent to align to a grid. Child elements do not
need to have any height or width settings; they will stretch to fill the space
of their cells automatically.

#### `grid-template`

The `grid-template` property is actually shorthand for two other properties,
`grid-template-columns` and `grid-template-rows`. These can be defined
separately, and if only one is defined, the other will be set to the default
value, `auto`. Because `grid` is designed to display elements in a single
column, setting `grid-template-columns` to `auto` or not setting it at all will
always produce just one column, whereas setting `grid-template-rows` to `auto`
will create as many rows as needed.

There are a number of units we can use in these template properties:

- `fr` - Represents a _fraction_ unit. Using `fr` will set a cell's width or
  height based on the total number of fractions used. A setting of
  `1fr 2fr 1fr 1fr` will result in each fraction being 20% of grid container,
  with the second cell being twice as large
- `%` - You can use percentages for each row or column in a template. These will
  act similar to `fr` units. It is possible to mix and match units in these
  templates
- `px` - Cells can be given a set width and height using the pixel unit. This
  can be helpful when you're creating more complex grids and want one row or
  column to stay the same size
- `auto` - The `auto` value can be used as the default value, but can also be
  used to set specific columns and rows. This works well with `px` and `%`
  units, so if we were to define `grid-template-columns` as `50px auto 25%`, we
  would get a three column grid where the first column is always 50 pixels wide,
  the last column is always 25% of the total width of our container, and the
  middle column will fill the remaining space

##### `repeat`

In addition to these, the template properties have a unique setting, `repeat`,
that makes definitions a little simpler. The `repeat` setting takes in two
arguments: the first is the amount of rows or columns you want; the second is
the size of those columns, using the units above. So if we wanted to recreate
our original `grid-template` using `repeat`, it would look like:

```css
grid-template: repeat(4, 1fr) / repeat(3, 1fr);
```

##### `[linenames]`

There is one more feature of the template properties worth exploring: when
defining a template of rows or columns, it is possible to give names to
specific lines in our grid. We do this by including these names in between
the unit values we're assigning, surrounded by square brackets, `[]`.

For example, if we wanted the first row of our grid to be where our 'header'
will go, we might write the following:

```
grid-template-rows: [header-start] 1fr [header-end] 1fr 1fr 1fr;
grid-template-columns: 1fr 1fr 1fr;

/* -or- */

grid-template: [header-start] 1fr [header-end] 1fr 1fr 1fr / 1fr 1fr 1fr;
```

The use of naming lines like this will become clearer later in this lesson.

#### `grid-auto-columns` and `grid-auto-rows`

If we need, we can also choose to define default sizes for our rows and grids
using `grid-auto-columns` and `grid-auto-rows`. These properties can take in
a length, or a unit such as `fr`, and apply this as the default for all cells
in a grid. So, for instance, if we added `grid-auto-rows: 50px;` to our
`.grid-container` class, our grid will shrink a bit, as each row will now be
exactly 50 pixels tall.

#### `grid-gap`

There is one other property we can choose to set on the parent element:
`grid-gap`. This property defines how much space is added in between cells. Go
back into our `index.css` file and add `grid-gap: 5px` to the `grid-container`
class. On our webpage, you'll see that each cell is now separated with
whitespace. Note that when using `grid-gap`, the cells will shrink a little to still fit
in the container. The `grid-gap` property can read pixel or percentage values.

## Reinforce What We've Learned About Grid

Just to recap, to get a grid up and running on a webpage, at minimum, you will
need one 'container' element. This element should `display` set to `grid` in its
styling.

Any child elements of this container will fit evenly into the rows of one
column. To make things a little more interesting, we need to use properties like
`grid-template` on the container element, arranging content into however many
rows and columns we like.

## Conclusion

CSS Grid allows us to set up a flexible grid-based page layout quickly and also
gives us various properties to customize the grid. If you need an efficient way
to build responsive websites, CSS Grid is a good modern tool.
