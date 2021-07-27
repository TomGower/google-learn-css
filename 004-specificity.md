# Specificity

## Specificity scoring

Each selector rule gets a scoring. Specificity is a total score, and each selector type earns points toward that score. Highest score wins.

In a real project, the key is making sure that that the CSS rules you expect to apply actually do apply, while keeping scores low to prevent complexity. The score should be as high as it needs to be, not as high as possible in case we need to override it with genuinely more important CSS later.

## Scoring each selector type

Each selector type gets points.

**Universal selector**: `*` gets 0 points.

**Element or pseudo-element selector**: an element/type `div` or pseudo-element `::selection` selector gets 1 point.

**Class, pseudo-class, or attribute selector**: a class selector (`.my-class`), pseudo-class selector (`:hover`), or attribute selector (`[href='#']`) gets 10 points of specificity.

By itself `:not()` adds nothing to the calculation. But the selector passed in as argument does get added to the calcuation. So `div:not(.my-class)` gets 11 points for specificity, 1 from `div` and 10 from `.my-class`.

**ID selector**: An ID selector gets 100 points of specificity as long as you use an ID selector (`#myID`) and not an attribute selector (`[id="myID"]`).

**Inline style attribute**: CSS applied directly to the `style` attribute of the HTML element gets 1000 points. `<div style="color: red"></div>`.

**`!important`**: An `!important` rule at the end of a CSS value gets 10,000 points. `!important` is applied to a CSS property, so everything in the overall rule does not get the same specifity score. Example:

```CSS
.my-class {
  color: red !important; /* 10,000 points */
  background: white; /* 10 points */
}
```

## Specificity in context

The specificity of each element that matches a selector is added together.

`a`: 1 point
`a.my-class`: 11 points
`a.my-class.another-class`: 21 points
`a.my-class.another-class[href]`: 31 points
`a.my-class.another-class[href]:hover` 41 points

## Visualizing specificity

In diagrams and specificity calculators, the specificity is often visualized like

ID - Class - Type
1 - 3 - 0

The left group is `id` selectors. The second group is class, attribute, and pseudo-class selectors. The final group is element and pseudo-element selectors. So `a.my-class.another-class[href]:hover` would be `0-4-1`.

Examples:
`section#specialty.dark`: 1-1-1
`#specialty:hover li.dark`: 1-2-1
`[data-state-rad].dark#specialty:hover`: 1-3-0
`li#specialty section.dark`: 1-1-2

## Pragmatically increasing specificity

Example HTML: `<button class="my-button" onclick="alert('hello')">Click me</button>`.

CSS #1:

```CSS
.my-button {
  background: blue;
}

button[onclick] {
  background: grey;
}
```

The second selector has 11 points of specificity, so it wins over `.my-button`'s 10 points. If you want to change that, repeat the class selector like this:

```CSS
.my-button.my-button {
  background: blue;
}

button[onclick] {
  background: grey;
}
```

`<button>` now has a blue background because `.my-button.my-button` gets a specificity score of 20 points (`0-2-0`).

WARNING: If you find you are needing to boost specificity by repeating classnames regularly, you may be writing overly specific selectors. Consider if you can refactor your CSS to reduce the specificity of other selectors to avoid the problem.

## Matching specificity scores see the newest win

Sample `<button>` HTML as before. CSS #3 example:

```CSS
.my-button {
  background: blue;
}

[onclick] {
  background: grey;
}
```

The `background: grey` is applied because both selectors have 10 points, so the we default to the order. If you change the order, then the background would be blue instead.
