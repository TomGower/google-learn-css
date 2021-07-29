# Grid

Grid gives a straightforward solution to the common web layout design of header, sidebar, body, and footer, with lots of options for how to do this.

## Overview

A grid can be defined with rows and columns. You can choose how to size the rows and column tracks or they can react to the size of the content.
Direct children of the grid will automatically be placed onto the grid.
Or you can place items in the precise location you want.
Lines and areas on the grid can be named to make placement easier.
Spare space in the grid container can be distributed between the tracks.
Grid items can be aligned within their areas.

## Grid terminology

Grid is the first real CSS layout system, so it has its own terminology.

**Grid lines**: A grid is made up of lines. That includes the "outside" lines, so a three-column layout will have four lines.

Lines are numbered starting from 1, with numbering following the writing mode and script direction of the component.

**Grid tracks**: A track is the space between two grid lines. A row track is between two row lines, and a column track is between two column lines. When we create our grid we create these tracks by assigning a size to them.

**Grid cell**: A grid cell is the smallest space on a grid defined by the intersection of row and column tracks. Akin to a table cell or cell in a spreadsheet. If you define a grid and don't place any of the items, they will automatically be laid out one item into each grid cell.

**Grid area**: Several grid cells together. Grid areas are created by causing an item to span over multiple tracks.

**Gaps**: The space between tracks. Cannot contain content, but you can span grid items across it.

**Grid container**: The element with `display: grid` applied that creates a new grid format content for the direct children.

**Grid item**: A grid item which is a direct child of the grid container.

## Rows and columns

Basic grid idea. Three columns, two rows, with gap:

```CSS
.container {
    display: grid;
    grid-template-columns: 5em 100px 30%;
    grid-template-rows: 200px auto;
    gap: 10px;
}
```

The dev tools can be useful for Chrome. In `Layout`, select `Display Line Numbers`.

### Intrinsic sizing keywords

Grid tracks can use the length and percentage dimensions described in Module 7 on sizing units. They can also use intrinsic sizing keywords. These include `min-content`, `max-content`, and `fit-content()`.

`min-content` will make a track as small as possible without the track content overflowing.
`max-content` will make a track wide enough for all of the content to display in one long unbroken string. This can cause overflows.
`fit-content()` works like `max-content` at first. Once the track reaches the size you pass into the function, the content starts to wrap. So `fit-content(10em)` will create a track that is up to 10em in width. If the track is less than 10em wide, it will be the width of the track. If the track is more than 10em wide, it will wrap.

### The `fr` unit

`fr` is a flexible unit that only works in grid and describes a share of the available space in the grid container.

It works similar to using `flex: auto` in flexbox. It distributes the space after the items have been laid out. `grid-template-columns: 1fr 1fr 1fr` will have three columns which each get the same share of available space.

If you want a component with a fixed size element and a variable size track, you can use `grid-template-columns: 200px 1fr`. (This is useful for something like the side/body layout that Grid is a good way to solve.)

### The `minmax` function

The function lets you set a minimum and maximum size for a track. You can use `minmax(auto, 1fr)` to distribute available space. Grid looks at the intrinsic size of the content, and distributes available space after giving the content enough room. But this doesn't mean each track gets an equal share of the space available in the grid container.

To force a track to take an equal share of the space in the grid container, you can set `minmax(0, 1fr)`. This makes the minimum size of the track 0 and not the min-content size.

### `repeat()` notation

If you want a twelve column layout, you could do:

```CSS
.container {
    display: grid;
    grid-template-columns:
      minmax(0,1fr),
      minmax(0,1fr),
      minmax(0,1fr),
      minmax(0,1fr),
      minmax(0,1fr),
      minmax(0,1fr),
      minmax(0,1fr),
      minmax(0,1fr),
      minmax(0,1fr),
      minmax(0,1fr),
      minmax(0,1fr),
      minmax(0,1fr);
}
```

or:

```CSS
.container {
  display: grid;
  grid-template-columns: repeat(12, minmax(0, 1fr));
}
```

You can use `repeat()` to repeat any section of your track listing. This can be used in combination with other lengths, like `grid-template-columns: 200px repeat(2, 1fr 2fr) 200px;`. This creates a six column layout of `200px 1fr 2fr 1fr 2fr 200px`.

### `auto-fill` and `auto-fit`

If you don't want to specify the number of column tracks, you can create as many as will fit in a given container. `grid-template-columns: repeat(auto-fill, 200px);` will create as many columns of 200px width as will fit in the container, whether that's 2 or 5. If you want that layout, but without leaving extra unfilled space, you can use `grid-template-columns: repeat(auto-fill, minmax(200px,1fr));`.

`auto-fill` and `auto-fit` act similarly but not the same. With `auto-fill`, items will be at the left side of the row as grid effectively creates "phantom" additional children of the described width. With `auto-fit`, no "phantom" additional children will be created and items will expand to fill all of the available space.

## Auto-placement

Auto placement is a common thing. Items will be added to the grid and occupy the next available grid cell. For many layouts this might be all you need.

### Placing items in columns

Default behavior is to place items along the rows. You can change this with `grid-auto-flow: column`. You need to define row tracks, otherwise the items will create intrinsic column tracks and layout all in one long row. This works in the writing direction of the document, so left to right in English and right to left in Arabic.

### Spanning tracks

You can cause specific items in an auto-placed layout to span more than one track. Use `span` plus the number of lines to span as a value for `grid-column-end` or `grid-row-end`. Example:

```CSS
.item {
    grid-column-end: span 2; /* will span two lines, therefore covering two tracks */
}
```

Because `.item` does not have a specified `grid-column-start`, this is aligned using the auto-placement rules. You can achieve the same result with `grid-column: auto / span 2`.

### Filling gaps

An auto-placed layout with some items spanning multiple tracks may result in some unfilled cells. The default behavior of grid is to always progress forward. The items will be placed in DOM order or any modification with `order`. If there is not enough space, it will leave an empty cell and move to the next track. E.g., in a three-column layout, if item three has `span 2`, 1 2 _ / 3 3 4 (my example).

Alternatively, you can set `grid-auto-flow: dense`. With this set, grid will take items later in the layout and use them to fill gaps. This may mean the visual display will be disconnected from the DOM order. (Going back to my example, 1 2 4 / 3 3 _.)

## Placing items

You can place items on the grid lines with `grid-column-start`, `grid-column-end`, `grid-row-start`, and `grid-row-end`. You can shorthand these properties with `grid-column` and `grid-row`. Example:

```CSS
.container {
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  grid-template-rows: repeat(2, 200px 100px);
}

.item {
  grid-column-start: 1; /* start at column line 1 */
  grid-column-end: 4; /* end at column line 4 */
  grid-row-start: 2; /*start at row line 2 */
  grid-row-end: 4; /* end at row line 4 */
}
```

### Stacking items

Using line-based position, you can place items onto the same cell of the grid. This means you can stack items or cause one item to partly overlap another. The default will be to place items later in the DOM order on top. You can change this stacking order using `z-index`.

### Negative line numbers

The explicit grid with `grid-template-rows` and `grid-template-columns` is one you have defined and given size to the tracks.

The implicit grid is when you might define column tracks and then add several rows of grid items without ever defining row tracks. The tracks would end up auto-sized by default. You might also place an item outside the explicit defined grid with `grid-column-end`. The grid will create tracks to make the layout work.

Most of the time, it doesn't matter if you're working with an explicit grid or an implicit grid. But with line-based placement, you might run into a difference.

You can use negative line numbers to place items relative to the end line of the implicit grid. You can make an item span from the first column to the last column in in explicit grid with `grid-column: 1 / -1`.

N.B. negative line numbers only work with the explicit grid.

**Implicit row size**: Tracks created in the implicit grid will be auto-sized by default. You can control the size of the rows with `grid-auto-rows` and the size of columns with `grid-auto-columns`.

Example: `grid-auto-rows: minmax(10em, auto);`
Example: `grid-auto-columns: 100px 200px;`

## Named grid lines

You can name any line on your grid by adding a name of your choosing between square brackets ([]). Multiple names can be added, separated by a space inside the same brackets. Once you have named lines, they can be used instead of the numbers.

```CSS
.container {
    display: grid;
    grid-template-columns:
      [main-start aside-start] 1fr
      [aside-end content-start] 2fr
      [content-end main-end]; /* a two column layout */
}

.sidebar {
    grid-column: aside-start / aside-end;
    /* placed between line 1 and 2*/
}

footer {
    grid-column: main-start / main-end;
    /* right across the layout from line 1 to line 3*/
}
```

## Grid template areas

You can also name areas of the grid and place items onto those named areas. Assign children names using `grid-area`. Set up the grid with `grid-template-areas`.

The rules:
The value must be a complete grid with no empty cells.
To span tracks repeat the name.
The areas created by repeating the name must be rectangular and cannot be disconnected.

To leave white space on a grid, use `.` or multiple `...` with no white space between them. Valid grid:

```CSS
.container {
    display: grid;
    grid-template-columns: repeat(4,1fr);
    grid-template-areas:
        "....... header header header"
        "sidebar content content content"
        "sidebar footer footer footer";
}
```

Grid template areas are defined based on the direction of the language. In a vertical rather than horizontal language, the 'top' row is on the left. In a RTL horizontal language, the empty cell in the above example would be on the right instead of the left.

## Shorthand properties

There are two shorthand properties you can use that will do most of it for you. But if you don't know them they can be confused. Whether you use them is up to you.

### `grid-template`

`grid-template` is a shorthand for `grid-template-rows`, `grid-template-columns`, and `grid-template-areas`. The rows are defined first, along with the value of `grid-template-areas`. Column sizing is added after a `/`. Example:

```CSS
.container {
    display: grid;
    grid-template:
      "head head head" minmax(150px, auto)
      "sidebar content content" auto
      "sidebar footer footer" auto / 1fr 1fr 1fr;
}
```

### `grid` property

`grid` shorthand can be used in the same way as `grid-template`. When used this way, it will reset the other grid properties to their default values. This include `g-t-r`, `g-t-c`, `g-t-areas`, `grid-auto-rows`, `grid-auto-columns`, and `grid-auto-flow`.

Alternately, you can use the shorthand to define how the implicit grid behaves. Example:

```CSS
.container {
    display: grid;
    grid: repeat(2, 80px) / auto-flow  120px;
}
```

## Alignment

Grid uses the same alignment properties as Flexbox.

In grid, the `justify-` properties are used on the inline axis, the direction in which sentences run in your writing mode (English, rows). The `align` properties are used on the block axis, the direction in which blocks are laid out in your writing mode (English, columns).

`justify-content` and `align-content`: distribute additional space in the grid container around or between tracks
`justify-self` and `align-self`: move a grid item around the grid area it is placed in
`justify-items` and `align-items`: set the `-self` property of all grid items

### Distributing extra space

N.B. gaps become larger when using values such as `space-between`, and any grid item spanning two tracks grows to absorb the additional space added to the gap.

Like flexbox, these properties only work when there is additional space to distribute.

### Moving content around

If your item is an image or something else with an intrinsic aspect ratio, the initial value of will be `start` rather than `stretch` to avoid stretching it out of shape.
