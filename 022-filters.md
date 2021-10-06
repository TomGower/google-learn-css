# Filters

If you need to build an element with a slightly opaque, frosted glass effect that sits over top of an image. The text needs to be live text and not an image. We can do this with a combination of CSS filters and `backdrop-filter` to apply effects and blur what's needed in real time. Blur and opacity are two of many available filters.

N.B. when placing text over images to make sure text is still readable should the filter effect not be supported in a user's browser. E.g., `backdrop-filter` is not supported by Firefox, so be sure that FF users are not left with text they cannot easily read.

## The filter property

`filter` can accept one of many values. If you incorrectly apply a filter, the rest of the filters defined for `filter` will not work.

### `blur`

E.g. `filter: blur(0.2em)`. This applies a gaussian blur. The only argument you can pass is a `radius`, which is how much blur is applied. This is a length unit, and cannot be a percentage.

### `brightness`

E.g. `filter: brightness(80%)`. This will increase or decrease the brightness of an element. The value is expressed as a percentage with the unchanged image being 100%. A value of `0%` turns the image completely black. Values over `100%` increase the brightness. It accepts decimal values in addition to percentages, so `80%` instead of `0.8`.

### `contrast`

E.g. `filter: contrast(160%)`. Set a value between 0% and 100% to increase or decrease the contrast. (Then explain why `160%` is a valid value.)

### `grayscale`

E.g. `filter: grayscale(80%)`. You can apply a completely grayscale effect using `1` as a value for `grayscale()` or `0` to have a completely saturated element. It accepts percentage or decimal values to apply a partial grayscale effect. With no arguments, the element will be completely grayscale. Values greater than `100%` will be capped at `100%`.

### `invert`

E.g. `filter: invert(1)`. Like `grayscale`, you can pass `1` or `0` to `invert()` to turn it on or off. When on, the element's colors are completely inverted. Also accepts percentage or decimal values to only apply a partial inversion of colors. With no arguments, the element will be completely inverted.

### `opacity`

E.g. `filter: opacity(0.3)`. The `opacity()` filter works just like the `opacity` property, where you can pass a number (decimal value) or percentage to increase or reduce opacity. If you pass no arguments, the element is fully visible.

### `saturate`

E.g. `filter: saturate(155%)`. The saturate filter is similar to the `brightness` filter and accepts the same argument, either a number (decimal value) or percentage. It increases or decreases the color saturation rather than increasing or decreasing the brightness effect.

### `sepia`

E.g. `filter: sepia(70%)`. Works like `grayscale()`, adds a sepia tone effect. The sepia tone is a photographic printing technique that converts black tones to brown tones to warm them up. Accepts a number (decimal value) or percentage to increase or decrease the effect. Passing no argument adds a full sepia effect, equivalent to `sepia(100%)`.

### `hue-rotate`

The hue in `hsl` references a rotation of the color wheel, as discussed in the Color lesson. If you pass an angle, which can be degree or turns, it shifts the hue of all the element's colors, changing part of the color wheel it references. Passing no argument does nothing.

### `drop-shadow`

E.g., `filter: drop-shadow(5px 5px 10px orange)`. Applies a curve-hugging drop shadow like you would with a design tool like Photoshop. The shadow is applied to an alpha mask which makes it very useful for adding a shadow to a cutout image. Takes a shadow parameter which contains space-separated offset-x, offset-y, blur, and color values. Almost identical to `box-shadow`, but the `inset` value and spread value are not supported. See more on the different types of shadows in the Shadows module.

### `url`

Allows you to apply an SVG filter from a linked SVG element or file.

## Backdrop filter

`backdrop-filter` accepts all of the same filter functions as `filter`. `backdrop-filter` applies only to the filters in the background, while `filter` applies to the whole element. The initial example of what you can do with a filter is an example of filters applied only in the background with `background-filter` and not to the entire element with `filter`.
