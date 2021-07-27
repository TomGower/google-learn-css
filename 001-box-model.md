# Box Model

Everything in CSS is a box, even if you use `border-radius` to make it look like a circle.

## Content and Sizing

Box size can be controlled using **extrinsic sizing** or you can let the browser set the size of the box for you based on the content size using **intrinsic sizing**.

Extrinsic sizing, how it goes wrong: box isn't big enough for the width of its content, text overflows.
Intrinsic sizing, how it goes wrong: image is displayed at full native size, taking up too much space on the screen.

## The Areas of the Box Model

Content on the inside.
Padding is the area around the content.
Border is the area around the padding.
Margin is the area around the border.

Background includes the padding.

Scrollbars live in the padding.

`outline` and `box-shadow` live in the margin.

## Controlling the box model

Default `display` values for a browser's user agent stylesheet:
`<div>`: `block`
`<li>`: `list-item`
`<span>`: `inline`

`inline`: block margin, but other elements won't respect it.
Use `inline-block` and other elements will respect block margin, most other `inline` behavior unchanged.

`block` will fill available *inline space*, but `inline` and `inline-block` will only be as large as their content.

By default, `box-sizing: content-box` is applied. That means `width` and `height` will be applied to the size of the **content box**. Any added `padding` and `border` will be added to the size of the content box to get the total size of the element.

Google quiz:

```CSS
.my-box {
  width: 200px;
  border: 10px solid;
  padding: 20px;
}
```

`.my-box` will have a width of 260px. 200px from `width`, and because of the default `box-sizing: content-box`, the `border` of 10px on each side and `padding` of 20px on each side will be added to that. `200 + 2 * 10 + 2 * 20 = 260`.

Alternate value: `box-sizing: border-box`. With this option, any `border` and `padding` get *pushed in*, so the size of the element up to the border will be 200px.

CSS reset for setting all elements to `border-box`:

```CSS
*,
*::before,
*::after {
  box-sizing: border-box;
}
```
