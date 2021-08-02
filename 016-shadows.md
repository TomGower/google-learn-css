# Shadows

Scenario: online store, picture of a T-shirt, cut out, with a drop shadow. T-shirt image is dynamic and can be updated via CMS, so drop shadow needs to be dynamic. Image doesn't have to be a T-shirt and could be anything else.

`box-shadow` and `text-shadow` are CSS properties. But image isn't text, so `text-shadow` doesn't work. `box-shadow` is on the surrounding box, not on the image itself. But you can use `drop-shadow()` filter. Those are the three CSS shadow properties, each used for a different purpose.

## Box shadow

`box-shadow` is used for adding shadows to the box of an HTML element. It works on both block elements and inline elements.

`box-shadow` can take 5 values. E.g., `box-shadow: 5px 5px 20px 5px #000;` In order:

1. Horizontal offset. Positive pushes out from left. Negative pushes it out from right.
2. Vertical offset. Positive pushes it down from top. Negative pushes it up from bottom.
3. Blur radius. Larger number produces a more blurred shadow. Small number produces a sharper shadow.
4. Spread radius. Optional. Larger number increases the size of the shadow. Smaller number decreases the size of the shadow. Same size as blur radius if set to 0.
5. Color. Any valid color value (`#000`, `goldenrod`, etc.). If undefined, computed text color will be used.

Default is an outer shadow. To make an inner shadow instead, use `inset` **before** other properties. E.g. `box-shadow: inset 5px 5px 20px 5px #000`.

### Multiple box shadows

You can add as many shadows as you like with `box-shadow`. Use comma separated values for each one. Example:

```CSS
.my-element {
  box-shadow: 5px 5px 20px 5px darkslateblue, -5px -5px 20px 5px dodgerblue,
    inset 0px 0px 10px 2px darkslategray, inset 0px 0px 20px 10px steelblue;
}
```

### Properties affect box-shadow

Adding `border-radius` will affect the shape of the box-shadow. This is because CSS is creating a shadow based on the shape of the box as if light is pointing at it.

If the box with `border-shadow` also has `overflow: hidden`, the shadow won't break out of that overflow either.

## Text shadow

`text-shadow` is similar to `box-shadow`, but it only works on text nodes.

`text-shadow` accepts the same values as `box-shadow` and in the same order. The only difference is `text-shadow` has no `spread` value and no `inset` keyword.

`box-shadow` is clipped to the shape of your box. `text-shadow` has no clipping. This means if your text is fully or semi-transparent, the shadow is visible through it.

### Multiple text shadows

Like `box-shadow`, `text-shadow` can have multiple shadows with comma separation. This can create cool effects, such as 3D text. Example:

```CSS
.my-element {
  text-shadow: 1px 1px 0px white,
    2px 2px 0px firebrick;
  color: darkslategray;
}
```

## Drop shadow

To achieve a drop shadow that follows any potential curves of an image, use the CSS `drop-shadow` filter. This shadow is applied to an alpha mask which makes it very useful for adding a shadow to a cutout image, as in the case in the intro of this module. Example:

```CSS
.my-image {
  filter: drop-shadow(0px 0px 10px rgba(0 0 0 / 30%))
}
```

Filters are covered in Module 22. In short, filters allow you to apply multiple graphical effects to the pixels of an element.

`drop-shadow()` accepts the same value as `box-shadow`, but does not accept the `inset` keyword and `spread` value.

You can add as many shadows as you like by adding multiple instances of `drop-shadow()` values to the `filter` property. Each shadow will use the last shadow as a positioning reference point.
