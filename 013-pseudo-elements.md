# Pseudo-elements

If you want the first letter to have a drop cap (that stupid enlarged capital letter), you can use the `::first-letter` pseudo-selector.

```CSS
p::first-letter {
  color: blue;
  float: left;
  font-size: 2.6em;
  font-weight: bold;
  line-height: 1;
  margin-inline-end: 0.2rem;
}
```

This lesson discusses which pseudo-elements are available and how to use them.

## `::before` and `::after`

Both `::before` and `::after` create a child element inside an element only if you define a `content` property.

```CSS
.my-element::before {
  content: "";
}

.my-element::after {
  content: "";
}
```

The content can be any string, even an empty string, but N.B. anything other than an empty string will be announced by a screen reader. You can add an image `url`, which will insert an image at its original dimensions and cannot be resized. You can also insert a `counter`. A `counter` can be named and incremented based on its position in the document flow. They can be useful for numbering an outline and in other contexts.

Once an element has been created with `::before` or `::after`, it can be styled like other elements. They only work with elements that will accept child elements, so elements such as `<img />`, `<video>`, `<button>`, and `<input>` will not accept them.

## `::first-letter`

Not all CSS properties can be used with `::first-letter`. The available properties are

-`color`
-`background` properties (such as `background-image`)
-`border` properties (such as `border-color`)
-`float`
-`font` properties (such as `font-size` and `font-weight`)
-text properties (such as `text-decoration` and `word-spacing`)

`::first-letter` can only be used on block containers. It won't work if you try to add it to an element that is `display: inline`.

## `::first-line`

Lets you style the first line of text. The element must have `display` value of `block`, `inline-block`, `list-item`, `table-caption`, or `table-cell`.

Similar to `::first-letter`, it only accepts some properties. These include `color`, `background` properties, `font` properties, and `text` properties.

## `::backdrop`

`::backdrop` lets you style the space between the element and the rest of the page if you have an element like `<dialog>` or `<video>` that is presented in full-screen mode.

`::backdrop` is not supported in Safari.

## `::marker`

`::marker` lets you style the bullet or number for a list item or the arrow of a `<summary>` element.

```CSS
::marker {
  color: hotpink;
}

ul ::marker {
  font-size: 1.5em;
}

ol ::marker {
  font-size: 1.1em;
}

summary::marker {
  content: '\002B'' '; /* Plus symbol with space */
}

details[open] summary::marker {
  content: '\2212'' '; /* Minus symbol with space */
}
```

`::marker` only supports some CSS properties. This includes `color`, `content`, `white-space`, `font` properties, and `animation` and `transition` properties. Using `content` lets you change the market symbol (as shown in the example above).

## `::selection`

`::selection` lets you choose how selected text is styled. It can be used to style all selected text. It can also be used in combination with other selectors for a more specific section style.

```CSS
p:nth-of-type(2)::selection {
  background: darkblue;
  color: yellow;
}
```

`::selection` only supports some CSS properties. These include `color`, `background-color` but not `background-image`, and `text` properties.

`::placeholder`

`placeholder` lets you add a helper hint to form elements like an `<input>`. You can style that placeholder text with `::placeholder`.

`::placeholder` only supports some CSS rules. These include `color`, `background` properties, `font` properties, and `text` properties.

N.B. `placeholder` is not a `<label>` and should not be used in place of a `<label>`. Form elements must be labeled or they will be inaccessible.

## `::cue`

`::cue` lets you style the WebVTT cues, which are the captions of a `<video>` element.

You can pass a selector into a `::cue`, which allows you to style specific elements *inside* a caption.

```CSS
video::cue {
  color: yellow;
}

video::cue(b) {
  color: red;
}

video::cue(i) {
  color: lightpink;
}
```
