# Layout

CSS gives us various ways to solve layout problems, on horizontal axis, vertical axis, or both.

## A brief history

`<table>` was the answer for how to lay out anything.

1996: CSS1, floats
1998: CSS2
2010: CSS3, responsive web design
2012: media queries, flexbox
2017: grid
2019: intrinsic web design
2021: container queries

## Layout: the present and future

We'll get to Flexbox and Grid in detail later. This is a high-level look at what we can do.

## Understanding the display property

`display` is either `inline` or `block`.
Inline: elements sit next to each other in the inline direction. `<span>` and `<strong>`, which are typically used to style text within a containing element like a `<p>`, are inline by default. They also preserve surrounding whitespace. Inline elements cannot have an explicity height and width. Any block-level margin and padding will be ignored by the surrounding elements.

Block: elements don't sit alongside each other, but create a new line for themselves. Unless changed by CSS, block elements will expand to the size of the inline dimension (width, normally). Margin on all sides of a block element will be respected.

`display` also determines how an element's children should display. `display: flex` makes the box a block-level box and converts its children to flex items.

## Flexbox and Grid

More detail later. Some detail for now.

### Flexbox

Flexbox is a mechanism for one-dimensional layouts. Layout a single axis, either horizontal or vertical. Default, children next to each other inline and stretched in the block, so they're all the same height.

Default: items will stay on the same axis and not wrap to a new line. `align-items` and `justify-content` will change location in the inline and block directions (they don't get into this here). `flex-wrap` can wrap content onto a new line.

Children of a `display: flex` element are Flex children. Alignment, order, and justification can be changed, as well as how they shrink or grow.

`flex: 1 0 auto` is shorthand for `flex-grow: 1; flex-shrink: 0; flex-basis: auto`. (I'm short-changing the Flexbox and Grid notes because this overview isn't necessarily interesting to me.)

### Grid

Flexbox: one-dimensional (single-axis) layouts.
Grid: multi-axis layouts.

Write layout rules on the `display: grid` element. Introduces `repeat()` and `minmax()`, plus `fr`.

## Flow layout

If not in Flexbox or Grid, elements use flow layout.

### Inline block

Inline elements normally don't have their margin and padding respected. Make them `display: inline-block` to change that. It gives a box some elements of a block element, but it still flows inline with the text.

### Floats

Floats are useful if you have an image within a paragraph of text, and you want the text to wrap around that image.

`float` tells an element to float to the direction specified, allowing other elements to wrap around it. Valid values include `left`, `right`, and `inherit`.

N.B. when you use `float`, any elements following the float element will have their layout adjusted. To prevent this, clear the float, by using `clear: both` on an element that follows your float element, or with `display: flow-root` on the parent of your floated elements.

### Multicolumn layout

If you have a long list of data to be displayed, you can make it display in multiple columns with `column-count: 2`, potentially with a `column-gap` between each column. Alternatively, you can set `column-width: 260px` (e.g.). Each column will be the width, and as the viewport expands, the number of columns will increase to fill the space. (Looking at this with their `<ul><li>` example, columns run vertically, then split. So AEI BFJ CGK DHL rather than ABC DEF GHI JKL.)

### Positioning

`position` changes how an element behaves in the normal flow of the document, and how it relates to other elements. Possible values are `relative`, `absolute`, `fixed`, and `sticky` in addition to the default `static`. Example:

```CSS
.my-element {
  position: relative;
  top: 10px;
}
```

In the above example, the element is moved 10px down based on its current position in the document, as it's position relative to itself.

Giving an element `position: relative` makes it the containing block of any elements with `position: absolute`.

Elements set with `position: absolute` break out of the current flow of the document. This means you can position the element where you want using `top`, `left`, `bottom`, and `right` in its nearest relative parent. All of the content surrounding the absolutely positioned element reflows to fill the remaining space left by that element.

`position: fixed` behaves similar to `absolute`, except with `<html>` as its parent element.

With `sticky`, you can have the anchored, fixed aspects of `sticky` and the more predictable flow-honoring aspects of `relative`.
