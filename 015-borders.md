# Borders

Between `padding` and `margin`, the 'frame' for the box of your element.

## Border properties

### Style

Define the `border-style` to get a border to appear. Options include `dotted`, `dashed`, `solid`, `double`, `groove`, `ridge`, `inset`, and `outset`.

With `ridge`, `inset`, `outset`, and `groove`, the browser will darken the border color for the second color to provide contrast and depth. How exactly the browser acts depends on the browser. In Chrome, they will appear solid. In Firefox, they will be lightened to then provide a second darker color. (I don't understand this explanation. Flipping between Chrome and Firefox for this page, I don't see a difference. Even looking at their image, I don't see a difference.)

Browser matters for other border styles too, like `dotted` and `dashed`. (Looking at their image, for Safari, `dotted`'s dashes appear more blocky than they do in very similar Chrome and Firefox. For `dashed`, Chrome's dashes are smaller and have less space between them. Dashes look very similar in Firefox and Safari.)

You can style each side of the box differently with `border-top-style`, `border-right-style`, `border-bottom-style`, and `border-left-style`.

### Shorthand

`border` can declare the border, and should be passed `border-width`, `border-style`, and `border-color`, in that order to do so. E.g. `border: 1px solid red`.

### Color

`border-color` can be used to set the color of the border. By default it uses the box's current text color, its `currentColor`. If you only declare border properties, like width, the color of that border will be the computed color.

Like `-style` you can use `-[side]-color` to set the color for a specific side.

### Width

How thick the border is. Default value is `medium` (I did not know this). Won't be divisible unless you define a style. Other options include `thin` and `thick`. Also accepts unit values, such as `px`, `em`, `rem`, or `%`.

Like `-style` and `-color`, you can use `-[side]-width` to set the width for a specific side.

## Logical properties

You can theoretically use `border-inline-end` and other logical properties to define the border instead of using the standard directions. Browser support for these properties varies, so check CanIUse and your test site before actually using in production.

## Border-radius

To give a box rounded corners use `border-radius`.

Like `margin` and `padding`, you can pass multiple values to `border-radius` and they will be interpolated into specific sides.

Similar to `-style`, `-color`, and `-width`, you can apply borders to specific corners with `border-[top/bottom]-[left/right]-radius`.

N.B. when you pass a single value to a specific corner, like `border-top-left-radius: 1em`, you're using another shorthand because a `border-radius` is split into two parts, the vertical and horizontal sides. The `border-top-left-radius` is setting both the 'border-top-left-top' radius and the 'border-top-left-left' radius. You can change these values by setting both, like `border-top-left-radius: 1em 2em`. The top left border is now an ellipse instead of the circular.

You can define these values in `border-radius` shorthand by using `/` to define the elliptical values after the standard values. This enables you to make complex shapes, like

```CSS
.my-element {
  border: 2px solid;
  border-radius: 95px 155px 148px 103px / 48px 95px 130px 203px;
}
```

## Border images

The border doesn't have to be a stroke, but can be any kind of image. This is set using `border-image`. You can set a source image, how that image is sliced, the image width, how far the border is outset from the edge, and how the border should repeat. Example:

```CSS
.my-element {
  border-image-source: url(https://assets.codepen.io/174183/border-image-frame.jpg);
  border-image-slice: 61 58 51 48;
  border-image-width: 20px 20px 20px 20px;
  border-image-outset: 0px 0px 0px 0px;
  border-image-repeat: stretch stretch;
}
```

`border-image-width` = `border-width` for images.

`border-image-outset` = the distance between the border image and the box that is wraps around (I need a visual example to get this and how it interacts with margin, and the MDN example isn't making me comfortable with how it works).

`border-image-source` can be a URL for any valid image, which includes CSS gradients. E.g. #1: see above. E.g. #2: `border-image-source: linear-gradient(to bottom, #000, #fff);`.

`border-image-slice` lets you slice an image into 9 parts, made up of 4 split lines. It works like `margin` shorthand where you can define top - right - bottom - left offset values. With offset values defined, you have 9 sections of the image: 4 corners, 4 edges, and 1 middle section. The corners of the image are applied to the corners of the element. The edges of the image are applied to the edges of the element. `border-image-repeat` defines how edges fill their space. `border-image-width` controls the size of the slices. The `fill` keyword determines whether the middle section is used by the element's background image or not.

`border-image-repeat` = how you would like your border image to repeat. It works the same as `background-repeat`. Possible values:
`stretch` = initial value, stretches the source image to fill available space where possible.
`repeat` = tiles the source image's edges as many times as possible, may clip edge regions to accomplish this.
`round` = same as repeat, except instead of clipping edge regions, it stretches the image as well as repeating it to achieve a seamless repeat.
`space` = same as repeat, except adds space between each edge region to create a seamless pattern.
