# CSS Grid Properties

## Problem Statement

There are various ways to build a responsive website layout. Choosing one can be
confusing and implementing it can be complicated. The best solution is one that
is quick, structured and comprehensive. Enter CSS Grid.

## Objectives

2.  Identify CSS Grid child element properties

### Adding Grid Properties to Child Elements

#### `grid-column-start`, `grid-column-end`, `grid-row-start`, and `grid-row-end`

So far, all of our properties have been assigned to the parent element of a
grid, but we can also add some properties to child elements to control how each
is arranged. To test this out, make a new CSS class called `bigItem` with
the following settings:

```css
.bigItem {
	grid-column-start: 1;
	grid-column-end: 3;
	grid-row-start: 1;
	grid-row-end: 3;
}
```

In our `index.html` page, choose any one of our child elements and add `bigItem`
as a second class to the element (`class="grid-item bigItem"`), save, and then
check out the page. Ah! Now we've got one big cell in the upper left corner
filled with just one div. All our other elements fill in the remaining space, in
order.

The start and end values here represent the lines between each grid item,
beginning from the far left and top of the container. So, the top line above
our first row equals 1, and that value increments for each additional line. A
single box in the upper left corner of our grid would extend from line 1 to
line 2 on both our rows and columns. Since we've set our `.bigItem` to start
on 1 and end on 3 for rows and columns, the box extends and fills the four grid
cells in the upper left corner. Change our settings in `.bigItem` to the
following, then refresh `index.html` in your browser to see the change:

```css
.bigItem {
	grid-row-start: 2;
	grid-row-end: 7;
	grid-column-start: 2;
	grid-column-end: 4;
}
```

Now, we've got a big central box with our remaining boxes fitting around the
top, left and bottom. Defining a value greater than the number of columns or
rows that are defined in our template will force the grid to extend out. This
can cause an issue in our grid, if, for instance, we've only defined behavior
for _4_ rows and 3 columns.

Grid cells in the fifth, six and seventh rows default to the height of their
content. We can fix this by modifying our `.grid-container` to include rules for
cells that have 'spilled over' into new rows.

If one of the start or end values is not entered, the size will always default
to one cell. So, given the settings above, if you took out `grid-row-end: 7;`, a box would be created that starts on the second row and only extends down
to the third.

Setting `grid-row-end` to `7` seems a little excessive, so let's set `bigItem`
to be a nice 2 x 2 cell:

```
.bigItem {
  grid-row-start: 2;
  grid-row-end: 4;
  grid-column-start: 2;
  grid-column-end: 4;
}
```

#### `grid-column`, `grid-row` and `grid-area`

The `grid-column-start`, `grid-column-end`, `grid-row-start`, and
`grid-row-end` are frequently used in conjunction, so CSS has provided
shorthand alternatives: `grid-column` and `grid-row`. We can replace the
existing `.bigItem` class with the following for the same effect:

```
.bigItem {
  grid-row: 2 / 4;
  grid-column: 2 / 4;
}
```

Both `grid-column` and `grid-row` take in two values, the start and end lines.

But wait! We can continue to reduce this. CSS provides another shorthand
option that replaces `grid-column` and `grid-row`: `grid-area`. The `grid-area`
property takes in _four_ values. In order, they are the start position for
row, the start position for column, the end position for row, and the end
position for column:

```
grid-area: <grid-row-start> / <grid-column-start> / <grid-row-end> / <grid-column-end>
```

We can then rewrite our `.bigItem` class as one line:

```
.bigItem {
  grid-area: 2 / 2 / 4 / 4;
}
```

Remember how it is possible to give _names_ to lines using our `grid-template`
properties? This is where these names become useful. If we had names for the
beginning and end rows of a page footer, for instance, we could declare a
`grid-area` for our footer as:

```
grid-area: footer-start / 1 / footer-end / 4
```

This would start our area wherever the line `footer-start` is defined in our
row template, and end wherever `footer-end` is defined. In a complex grid,
taking the time to name important lines in your layout makes it easier to
position grid elements to them without having to look up or count the number of
lines.

#### `justify-self` and `align-self`

Grid has two additional properties that affect the contents of grid elements.
The `justify-self` and `align-self` properties define where, within a grid
cell, an element will be positioned. Using these properties will stop grid
from automatically expanding an element to fill the entire cell.

Let's add to our `.bigItem` class to see this in action by changing the class
properties to the following:

```
.bigItem {
  grid-area: 2 / 2 / 4 / 4;
  height: 50%;
  width: 50%;
  justify-self: center;
}
```

Here, we've shrunk our element down to half the width and height of the
`grid-area` we've defined. Using `justify-self: center`, this smaller
box is now moved horizontally to the middle of the area. To center vertically,
we can add `align-self: center` and the box will be perfectly centered
within the defined `grid-area`. The `justify-self` and `align-self` properties
can be set to align to the `start` or `end` of an element, as well as `stretch`
to fit the space, or even align to the `baseline` of inner text.

We can also choose to apply these justify and align rules to the entire grid
using two properties on the parent element: `justify-items` and `align-items`.

## Reinforce What We've Learned About Grid

To get fine tuned with specific content, we can apply styling to child elements,
overriding template rules.

The tests in this lesson are in place to practice what we have discussed.

- In `index.css`, the `.gridContainer` class should have `display` and
  `grid-template` properties correctly assigned
- In `index.css`, there should be a `.bigItem` class with a `grid-area`
  property assigned
- In `index.html`, the `bigItem` class should be assigned to one of the divs

Run `learn` to confirm you have correctly applied CSS Grid properties. If the
test pass, enter `learn submit`. You'll then be prompted to move on!
