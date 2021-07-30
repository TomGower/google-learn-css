# Logical Properties

Common user interface pattern: text label with supporting inline icon. Basic idea: some icon with some `margin-right`, then text. But in RTL language like Arabic instead of English, this throws off our alignment. Logical properties let us solve this problem.

## Terminology

Top, right, bottom, and left refer to physical dimensions of our viewport. Logical properties instead refer to the *flow of content*, which means they change if the text direction or writing mode changes.

## Block flow

Block flow is the direction in which content blocks are placed. Example: `<p><p>`. In English/LTR, these are aligned vertically, top to bottom.

## Inline flow

Inline flow is how text flows in a sentence. English is LTR. Arabic is RTL. The initial value for `writing-mode` is `horizontal-tb` (looking it up, `tb` stands for 'Top to Bottom', the direction of block flow). Alternatively, you can use `vertical-rl` or `vertical-lr`. These can be applied to the document as a whole or to specific elements with `writing-mode`.

## Flow relative

With logical properties, use `margin-block-start` instead of `margin-top` (as it would be in English).
`margin-bottom` = `margin-block-end`
`margin-left` = `margin-inline-start`
`margin-right` = `margin-inline-end`

N.B. `margin` is just the example. Also works the same for `padding` and `border`.

## Sizing

`max-width` and `max-height` assume a certain screen orientation. You can replace these with logical properties.

`max-width` = `max-inline-size`
`min-width` = `min-inline-size`
`max-height` = `max-block-size`
`min-height` = `min-block-size`

## Start and end

To align text to the right, `text-align: right`. In logical properties, `text-align: end`.

## Spacing and positioning

Directions:

```CSS
.my-element {
  padding-top: 2em;
  padding-bottom: 2em;
  margin-left: 2em;
  position: relative;
  top: 0.2em;
}
```

Logical properties:

```CSS
.my-element {
  padding-block-start: 2em;
  padding-block-end: 2em;
  margin-inline-start: 2em;
  position: relative;
  inset-block-start: 0.2em;
}
```

## Borders

`border` and `border-radius` can also be done with logical properties. Two ways to do the same thing:

```CSS
.my-element {
  border-bottom: 1px solid red;
  border-right: 1px solid red;
  border-bottom-right-radius: 1em;
}
.my-element {
  border-block-end: 1px solid red;
  border-inline-end: 1px solid red;
  border-end-end-radius: 1em;
}
```

`border-end-end` = 'block end' and 'inline end'.

## Units

`vw` and `vh` are based on a certain viewport alignment, and like other directional properties, have their own logical property equivalents.

`vw` = `vi`, 1% of the viewport size in the inline direction.
`vh` = `vb`, 1% of the viewport size in the block direction.

Those units will always map to the reading direction.

(These seem less useful than the other logical properties. I can see how in some cases, you might want to use, say, `80vi` to better display a large piece of written next. But in other cases, it really matters how wide and tall the screen size is, and you want to do things based on that. But maybe my brain just isn't translating well to the different challenges of building layouts on different writing directions.)

## Using logical properties pragmatically

Logical properties aren't just for internationalization. One problem: you want a chart with labels on the X and Y axes. Give the Y-axis label `writing mode: vertical-rl`, and use the same `margin` values on both labels using logical properties. You can give both axes `margin-block-start` to separate them from the graph itself.

## Solving the icon issue

Instead of `margin-right`, use `margin-inline-end`.

## Browser Support

It's kind of complicated. Some browsers accept everything, some don't accept some of the shorthand properties. Can CanIUse before deploying.
