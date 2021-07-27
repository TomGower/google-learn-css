# Selectors

Sample CSS rule:

```CSS
.my-css-rule {
  background: red;
  color: beige;
  font-size: 1.rem;
}
```

Selector: `.my-css-rule`
Declaration: `color: beige;`
Property: `color`
Value: `beige`

## Simple selectors

The most straightforward group of selectors target HTML elements plus classes, IDs, and other attributes which may be added to an HTML tag.

### Universal selector

A.k.a the wildcard. `*` matches any element.

### Type selector

A type selector, like `section`, matches an HTML element directly.

### Class selector

The class selector matches any element that has that class applied to it, like `.my-css-rule` in the above example.

The value of a CSS class element can be almost anything, but it cannot start with a number. The same is also true of IDs.

### ID selector

An HTML element with an `id` attribute should be the only element on a page with that ID value.

```HTML
<style>
  #rad {
    border: 1px solid blue;
  }
</style>
<div id="rad"></div>
```

The browswer will apply the CSS for `#rad` to all elements with `id="rad"`. But any element with `id=` is supposed to have a unique value for it, so unless you're writing very specific CSS for a single element, avoid applying styles with the `id` selector as it means you can't re-use those styles elsewhere.

### Attribute selector

You can look for elements that have a certain HTML attribute, or have a certain value for an HTML attribute, using the attribute selector. See [MDN](https://developer.mozilla.org/en-US/docs/Web/CSS/Attribute_selectors). Wrap the attribute in `[]`. Example:

```HTML
<style>
  [data-type='primary'] {
    color: red;
  }
</style>
<div data-type="primary"></div>
```

Alternatively:

```HTML
<style>
  [data-type] {
    color: red;
  }
</style>
<div data-type="primary"></div>
<div data-type="secondary"></div>
```

If you need the attribute selector to be case-sensitive, add `s` to the attribute selector. Example:

```HTML
<style>
  [data-type='primary' s] {
    color: red;
  }
</style>
<div data-type="primary">red</div>
<div data-type="Primary">not red</div>
```

If you specifically want it to be insensitive, you can add `i` to the attribute selector.

You can also match portions of strings inside attribute values. Example:

```CSS
/* A href that contains “example.com” */
[href*='example.com'] {
  color: red;
}

/* A href that starts with https */
[href^='https'] {
  color: green;
}

/* A href that ends with .com */
[href$='.com'] {
  color: blue;
}
```

### Grouping selectors

Group selectors by separating them with commas. Example is:

```CSS
strong,
em,
.my-class,
[lang] {
  color: red;
}
```

Q: does each selector have to be on separate lines, or will they work if all on the same line? A quick test confirms they can all be on the same line and it'll work, so having them on separate lines is just good practice.

## Pseudo-classes and pseudo-elements

CSS also includes selector types that focus in specific platform state, like when an element is hovered, structures inside an element, or parts of an element.

### Pseudo-classes

You can apply styles just when an element or one of its children is hovered by the use with a mouse pointer with `:hover`.

Pseudo-classes will be covered in more detail later.

### Pseudo-elements

Instead of responding to platform state like pseudo-classes, pseudo-elements act like they are inserting a new element within CSS. They also feature using the `::` double colon instead of `:`. But this last distinction wasn't always the case, so if you're supporting an old platform like IE8, you can use `:before` and `:after`.

Example:

```CSS
.my-element::before {
  content: 'Prefix - ';
}
```

The `::before` pseudo-element is used to insert content at the start of an element. You can also use the `::after` pseudo-element to insert content at the end of an element.

Pseudo-elements can also be used to target specific parts of an element.

```CSS
/* Your list will now either have red dots, or red numbers */
li::marker {
  color: red;
}
```

Alternatively, `::selection` can be used to style content that has been highlighted by a user.

```CSS
::selection {
  background: black;
  color: white;
}
```

Like pseudo-classes, pseudo-elements get their own module later.

## Complex selectors

Because CSS can only look down (see the later module on the cascade), we can use more complex selectors to help us target specific elements.

### Combinators

A descendant combinator lets us target a child element. The uses a ` ` space to look for child elements.

```CSS
p strong {
  color: blue;
}
```

A descendant combinator will naturally select all child elements of that type of that given parent element. Example I came up with:

```HTML
<style>
  p {
    color: blue;
  }
  div strong {
    color:red;
  }
</style>
<div>
  <strong>This text will be red.</strong>
  <p>This text will be blue. <strong>But this text will be red.</strong></p>
</div>
```

Their example:

```HTML
<style>
  .top div {
    padding-left: 2em;
  }

  .top p {
    background: #fff;
    padding: 0.5em;
  }
</style>
<div class="top box">
  <div>
    <p>1 level deep</p>
    <div>
      <p>2 levels deep</p>
      <div>
        <p>3 levels deep</p>
      </div>
    </div>
  </div>
</div>
```

'1 level deep` has 2em of padding. '2 levels deep' has 4em of left padding. '3 levels deep' has 6em of left padding.

With the sibling combinator, you can look for an element that immediately follows another element by using a `+` character in your selector.

```HTML
<style>
  .top * + * {
    margin-top: 1.5em;
  }
</style>
<div class="top box">
  <p>I have no margin because I am the first child.</p>
  <p>
    I have <code>margin-top</code> because I am a <strong>next sibling</strong>.
  </p>
  <p>I am also a <strong>next sibling</strong>, so also get margin top.</p>
</div>
```

The second and third paragraphs both have `margin-top`.

You could add margin to all child elements of `.top` with the selector `.top *`. But you probably don't need or want top margin on the first element. Using the *sibling combinator* mixed with the *universal selector* enables you to control not only what elements get space, but also apply to any element. This gives you long-term flexibility for what type of elements are children of `.top`.

The subsequent-sibling combinator is similar to the next sibling combinator. It uses `~` instead of `+`. For it to work, an element just has to follow another element with the same parent, rather than being the next element with the same parent. (Their example here stinks, in that I can't recreate and play with it myself because they're pulling in legit styling from elsewhere.)

The child combinator, or direct descendant combinator, gives you more control over the recursion that comes with combinator selectors. By using `>`, you can limit the combinator to apply only to direct children.

Going back to my example:

```HTML
<style>
  p {
    color: blue;
  }
  div > strong {
    color:red;
  }
</style>
<div>
  <strong>This text is still red.</strong>
  <p>This text is still blue. <strong>This text is now blue instead of red.</strong></p>
</div>
```

Their example:

```HTML
<style>
  .top * + * {
    margin-top: 1.5em;
  }

  em {
    display: inline-block;
  }
</style>
<div class="top box">
  <p>I have no margin because I am the first child.</p>
  <p>
    I have <code>margin-top</code> because I am a <strong>next sibling</strong>.
  </p>
  <p>
    I have a <strong>bold</strong> <em>then an emphasised bit of text</em>,
    which because I put <code>inline-block</code> on my emphasised text, gives
    us unwanted spacing.
  </p>
</div>
```

If we change the `margin-top` selector to `.top > * + *`, then our selector applies only to direct children of `.top` and our problem goes away. (I like my explanation better, even though it has its own cascade-related problem.)

### Compound selectors

You can combine selectors to increase specificity and readability. For example, `a.my-class` applies only to `<a>` elements that also have a `class="my-class"`.
