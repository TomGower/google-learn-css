# Spacing

Imagine three boxes. You want space between them. How many ways might you do that?

There are many. `margin`, but you don't want margin on all of them. (Padding! Wide clear border! CSS selectors to be precise! Top/bottom on each of margin/border/padding! If it's spaced right, it works.) `gap` might be more appropriate. All the solutions have strengths and caveats.

## HTML spacing

`<br>` and `<hr>` let you space elements in the block direction (vertically in English).

`<br>` is a line break.
`<hr>` creates a horizontal line with space on either side, with inherent `margin`.

HTML entities can also create space. HTML entities are reserved strings of characters that are replaced with character entities by the browser. E.g., `&copy;` = ©️. `&nbsp;` = a non-breaking space character, which provides inline space. N.B. the non-breaking aspect stitches two elements together, which can result in odd behavior.

N.B. use HTML elements only when the space helps with the understanding of the document. `<hr>` doesn't just add space. It creates a logical separation of two chunks of content. If you just want a line with space around it, adding a border with CSS might be more appropriate.

## Margin

If you want space around the outside of an element, use `margin`. By itself, `margin` is shorthand for `-top`, `-right`, `-bottom`, and `-left`. You can give margin one to four values.

One value: applied to all sides.
Two values: first value applied to top/bottom, second value applied to right/left.
Three values: first value applied to top, second value applied to right/left, third value applied to bottom.

Margin can be defined with a length, percentage, or auto value. If you use a percentage, the value will be calculated based on the width of the containing block.

For block level elements with a restricted size, `margin: auto` will take up available space in the direction that it is applied to. We saw this in Module 9: Flexbox, where we used `margin-left: auto` to move a single element to the right side, away from the other two elements.

Another `margin: auto` example is a horizontally centered wrapper with a max width.

```CSS
.wrapper {
  max-width: 400px;
  margin: 0 auto;
}
```

This element will occupy the 400px in the center of the screen.

### Negative margin

Margin accepts negative values. This will reduce space between elements. This can result in overlapping elements if you declare a negative value that's more than the available space.

### Margin collapse

Example:

```HTML
<style>
  h1 {
    margin-bottom: 2rem;
  }
  p {
    margin-top: 3rem;
  }
</style>
<article>
  <h1>My heading with teal margin</h1>
  <p>A paragraph of text that has blue margin on it, following the heading with margin.</p>
</article>
```

What's the margin between `<h1>` and `<p>`? You might think 5rem because of the two margins. But it's actually 3rem, because the CSS algorithm only cares about the larger margin value.

Only block margins collapse, not inline (horizontal) margins.

Margin collapse goes back to when the web was mostly documents. Collapsing margins helped set consistent spacing between elements and reduced the creation of huge gaps between adjacent elements that both have margin defined.

Margin collapse also helps with empty elements. If an empty element has `margin-top: 20px; margin-bottom: 20px`, it will only be 20px tall, not 40px.

You can prevent margin collapse by giving an element `position: absolute`. Using `float` will also eliminate margin collapse.

Using elements with no margin between two elements with margin will also prevent margin collapse, because the two elements with collapsing margin will no longer be adjacent.

If we take the above example and make it a Flexbox container with `flex-direction: column`, both the top and bottom margin will be respected.

For more on margins, see [Rachel Andrews' piece](https://www.smashingmagazine.com/2019/07/margins-in-css/).

## Padding

`margin` creates space on the outside of the box. `padding` creates space on the inside of the box. Depending on the box model, `padding` either might or might not affect the overall dimensions of the element (`content-box` yes, `border-box` no).

Like `margin`, `padding` is shorthand for `-top`, `-right`, `-bottom`, and `-left`. It also also accepts logical properties, so `-block-start`, `-inline-end`, `-block-end`, and `-inline-start` (and multiple values, treated the same way).

## Positioning

Any value other than `position: static` can also be spaced with `top`, `right`, `bottom`, and `left`.

`position: relative` will maintain its place in the document flow, even with directions set. The directions will behave relative to the element's natural position.
`position: absolute` will base the directional values from the relative parent's position.
`position: fixed` will base the directional values on the viewport.
`position: sticky` will only apply the directional values when it is in its docked/stuck state.

Instead of directions, you can use the logical properties `inset-block` and `inset-inline`. Two values for both top/bottom and right/left or one for all four.

## Grid and flexbox

`gap` separates elements in both Grid and Flexbox. `gap` is shorthand for `row-gap` and `column-gap`. One value is both. Two values, `row` is the first and the second goes to `column`.

You can also use Flexbox and Grid properties to create space between elements (`space-around`, etc), as discussed in those Modules.

## Creating consistent spacing

It's a good idea to pick a strategy and stick with it to create a consistent user interface with good flow and rhythm. A good way to do this is to use consistent measures for your spacing. E.g., commit to `20px` as a consistent measure for all gutters. Or `1em` as the vertical spacing between flow content, so it's responsive to changes in `font-size`. Whatever you choose, it's a good idea to save these values as variables or CSS custom properties to tokenize those values and make consistency a bit easier.

Example:

```CSS
:root {
  --gutter: 20px;
  --spacing: 1em;
}

h1 {
  margin-left: var(--gutter);
  margin-top: var(--spacing);
}
```
