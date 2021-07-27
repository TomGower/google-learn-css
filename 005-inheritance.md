# Inheritance

Imagine this HTML: `<a href="http://example.com" class="my-button">I am a button link</a>`. And give it this CSS:

```CSS
.my-button {
  display: inline-block;
  padding: 1rem 2rem;
  text-decoration: none;
  background: pink;
  font: inherit;
  text-align: center;
}
```

But in their example (which is complicated), `article a { color: maroon; }` has overridden the text of that link to make it maroon.

## Inheritance flow

HTML:

```HTML
<html>
  <body>
    <article>
      <p>Lorem ipsum dolor sit amet.</p>
    </article>
  </body>
</html>
```

The root element (`<html>`) won't inherit anything because it is the first element in the document. Add some CSS to `html` and it will start to cascade down the document:

```CSS
html {
  color: lightslategray;
}
```

The lorem ipsum text will now be `lightslategray` because `color` property is inheritable. CSS example #2:

```CSS
body {
  font-size: 1.2em;
}
```

This will cascade down to the text, so it will be at size 1.2em. But because `body` is the selector, it will still have the initial font size set by the browser (user agent stylesheet). But `body`'s children `article` and `p` will inherit the `font-size`.

CSS example #3:

```CSS
p {
  font-style: italic;
}
```

Only `<p>` will have italic font. `<body>` and `<article>` will have the font style set by the browser (user agent stylesheet).

Full list of inheritable properties: `azimuth`, `border-collapse`, `border-spacing`, `caption-side`, `color`, `cursor`, `direction`, `empty-cells`, `font-family`, `font-size`, `font-style`, `font-variant`, `font-weight`, `font`, `letter-spacing`, `line-height`, `list-style-image`, `list-style-position`, `list-style-type`, `list-style`, `orphans`, `quotes`, `text-align`, `text-ident`, `text-transform`, `visibility`, `white-space`, `widows`, and `word-spacing`. (I definitely have not used close to all of these properties.)

## How inheritance works

Every HTML element has every CSS property defined by default with an initial value. The initial value is a property that's not inherited and shows up as a default if the cascade fails to calculate a value for that element. Inheritable properties cascade downward and child elements get a computed value which represents its parent's value. If a parent has `font-weight: bold`, all child elements will be bold unless their `font-weight` is set to a different value or the user agent stylesheet has a value for `font-weight` for that property.

## How to explicitly inherit and control inheritance

### The `inherit` keyword

You can make any property inherit its parent's computed value with `inherit`. A useful way to use this keyword is to create exceptions. Sample CSS:

```CSS
strong {
  font-weight: 900;
}
.my-component {
  font-weight: 500;
}
.my-component strong {
  font-weight: inherit;
}
```

Normal bold text will have `font-weight: 700`, so `strong` elements will be stronger than that. The last declaration, `.my-component strong` ensures that all `strong` text inside `.my-component` shares `.my-component`'s `font-weight: 500`, not the `font-weight: 900` declared in `strong`.

### The `initial` keyword

The `initial` keyword lets you set a property back to that initial default value. Example:

```CSS
aside strong {
  font-weight: initial;
}
```

That CSS removes the bold weight from `<strong>` inside `<aside>` and instead gives them the initial value, which is normal weight.

### The `unset` keyword

`unset` behaves different based on whether the property is inheritable. If the property is inheritable, it will work the same way as `inherit`. If the property is not inheritable, it will work the same way as `initial`. Example:

```CSS
/* Global color styles for paragraph in authored CSS */
p {
  margin-top: 2em;
  color: goldenrod;
}

/* The p needs to be reset in asides, so you can use unset */
aside p {
  margin: unset;
  color: unset;
}
```

In `<p>` in `<aside>`, the `margin` is removed and `color` reverts back to the inherited computed value.

In that example, if you add to `p` additional properties, like `padding: 2em; border: 1px solid`, those will not be reset by the above example. But you can add `all: unset` to `aside p` and they will be.
