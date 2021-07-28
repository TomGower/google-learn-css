# Sizing Units

To limit line length and improve readability, you can use the `ch` unit. The `ch` unit is based on the width of `0` in the current font size, and gives you the ability to limit the width of text with a unit that's designed to size text. That permits predictable control regardless of the size of the text. Sample usage: `max-width: 70ch`.

## Numbers

Numbers are used to define `opacity`, `line-height`, and `rgb` color channel values. They can be unitless integers or decimals.

The meaning of numbers differs based on their context. In `line-height`, a number is representative of a ratio if you define it without a supporting unit. With `font-size: 24px; line-height: 1.5`, the line height is 36px, 1.5 * 24, a ratio based on the element's computed pixel size.

`line-height` is a good property to give a unitless value. `font-size` can be inherited, so using a unitless value means the line-height will always be related to its font-size. Giving it a fixed value of `16px` wouldn't look good if its unit inherited `font-size: 24px` (my example, can confirm this looks dumb after testing it).

Numbers can also be used:
-When setting values for filters. `filter: sepia(0.5)` applies a 50% sepia filter.
-When setting opacity. `opacity: 0.5` applies 50% opacity.
-In color channels. `rgb(255, 140, 0)` accepts values 0-255, as detailed on Module 6 on Color.
-To transform an element. `transform: scale(1.2)` scales the element by 120% of its initial size.

## Percentages

When using a percentage in CSS, you need to know how the percentage is calculated. E.g., `width` is calculated as a percentage of the width of the parent element:

```CSS
div {
  width: 300px;
  height: 100px;
}

div p {
  width: 50%; /* calculated: 150px */
}
```

If you set `margin` or `padding` as a percentage, they will be a portion of the **parent element**'s width, regardless of direction. Example:

```CSS
div {
  width: 300px;
  height: 100px;
}

div p {
  margin-top: 50%; /* calculated: 150px */
  padding-left: 50%; /* calculated: 150px */
}
```

If you set a `transform` value as a percentage, it is based on the element with the transform set. In this example, `<p>` has a `translateX` of `10%` and `width: 50`. `<p>`'s parent element width is 300px, so `<p>`'s width is 150px. 10% of 150px is 15px, so this is `translateX: 15px`. Example:

```CSS
div {
  width: 300px;
  height: 100px;
}

div p {
  width: 50%; /* calculated: 150px */
  transform: translateX(10%); /* calculated: 15px */
}
```

## Dimensions and length

If you attach a unit to a number, it becomes a dimension. The unit is called a *dimension token*.

Lengths are dimensions that refer to distance, and they can be absolute or relative.

### Absolute lengths

All absolute lengths resolve against the same base, making them predictable whenever they're used. Example:

```CSS
div {
  width: 10cm;
  height: 5cm;
  background: black;
}
```

You should be able to take a ruler to the screen and accurately measure the width and height of `<div>`. This is most useful when styling print content (which Wes Bos mentioned in an old Syntax.fm episode I listened to lately, about printing envelopes).

Absolute units: `cm`, `mm`, `Q` (quarter-millimeters), `in`, `pc` (Picas, 1/6"), `pt` (Points, 1/72"), `px` (Pixels).

### Relative lengths

Relative lengths are calculated against a base value, like a percentage. The difference between these and percentages is you can contextually size elements. Relative lengths are particularly useful on the web because of responsiveness.

#### Font-size-relative units

These units are relative to the size of elements of rendered typography, such as the size of text (`em`) or the width of typefaces (`ch`).

`em`: relative to the base computed font size of the element
`ex`: heuristic to determine whether to use the x-height, a letter "x", or '.5em' in the current computed font size of the element.
`cap`: height of the capital letters of the current computed font size of the element.
`ch`: average [character advance](https://www.w3.org/TR/css-values-4/#length-advance-measure) of the narrow glyph in the element's font.
`ic`: average character advance of the full width glyph in the element's font, as represented by the "水" (CJK water ideograph, U+6C34) glyph.
`rem`: font size of the root element (default 16px).
`lh`: line height of the element.
`rlh`: line height of the root element.

#### Viewport-relative units

You can use the dimensions of the viewport as a relative basis. These units portion up the available viewport space.

`vw`: 1% of the viewport's width. Resize a header font based on the width of the page as the user resizes.
`vh`: 1% of the viewport's height. Arrange items in the UI, like a footer toolbar.
`vi`: 1% of the viewport's size in the root element's inline axis. Horizontal in English. Vertical in a vertical writing language like some Japanese typefaces.
`vb`: 1% of the viewport's size in the root element's block axis. Vertical in English. Horizontal in a vertical writing language like some Japanese typefaces.
`vmin`: 1% of the viewport's smaller dimension.
`vmax`: 1% of the viewport's larger dimension.

Relative units like `rem` will respect a user-set font size. Fixed units like `px` will ignore those preferences.

## Miscellaneous units

There are other units, which have been specified to deal with particular types of values.

### Angle units

We saw angle units in the color module. They are also useful for rotating elements within transform functions.

```CSS
div {
  width: 150px;
  height: 150px;
  transform: rotate(60deg);
}
```

Using `deg`, you can rotate a `<div>` 90deg on its center axis.

```CSS
div {
  background-image: url('a-low-resolution-image.jpg');
}

@media (-webkit-min-device-pixel-ratio: 2), (min-resolution: 192dpi) {
  div {
    background-image: url('a-high-resolution-image.jpg');
  }
}
```

Other angle units include `rad` (radians), `grad` (gradians), and `turn` units, which represent part of an angle. `1turn` = `360deg`.

### Resolution units

a
