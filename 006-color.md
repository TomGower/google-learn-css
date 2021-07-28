# Color

## Numeric Colors

Numeric colors are probably the most common way to be exposed to CSS colors. Numeric color values come in a couple different forms.

### Hex colors

Sample: `color: #b71540`.

Hexadecimal notation is a shorthand for RGB, which assigns a numeric value to red, green, and blue, the three primary colors. When used in a six-digit sequence, they are translated to RGB numerical ranges, which are 0-255 for each of the primary colors. So `b71540` is 183 Red - 21 Green - 64 Blue.

You can also define an alpha value, convering the degree of transparency, with any numerical colors. In hex code, add another two digits to the six digit sequence, making an 8-digit sequence.

Example: black in hex is `#000000`. To make it 50% transparency, add `80` for `#00000080`. Because hex is weird, the transparency values are not what you'd expect. But 0% is `00`, 50% is `80`, and 75% is `BF` (191, or .75 * 255).

You can also write hex codes in 3-digit shorthand. A three digit hex code is a shortcut to an equivalent six digit sequence. So `#a4e` is the same as `#aa44ee`. You can include alpha by adding a fourth character, so `#a4e8` would expand to `#aa44ee88`.

### RGB (Red, Green, Blue)

Sample: `color: rgb(183, 21, 64)`.

RGB colors are defined with the `rgb()` function. You can pass in as parameters either numbers on a 0-255 range or percentages between 0-100%.

Black is `rgb(0, 0, 0)` (or `0%, 0%, 0%`). White is the exact opposite, `rgb(255, 255, 255)` (or `100% 100% 100%`).

To set alpha using RGB, you have two options. One, you can either add a `/` after the rgb values, like `rgb(0 0 0 / 50%)` to set 50% transparency on black. Second, for wider support, use the `rgba()` function. To set 50% transparency on black, use `rgba(0, 0, 0, 50%)` or `rgba(0, 0, 0, 0.5)`.

Newer color functions, such as `lab()` and `lch()` uses spaces instead of commas as a delimiter, so older functions like `rgb()` and `hsl()` no longer require commas as a delimiter. For better backwards compatability, you can still use commas to define `rgb()` and `hsl()`.

### HSL (Hue, Saturation, Lightness)

Sample: `hsl(344, 79%, 40%)`.

Hue describes the value on the color wheel, from 0 degrees to 360 degrees, starting with red (both 0/360). A hue of 180 or 50% would be in the blue range.

Saturation is how vibrant the selected hue is. A fully desaturated color (0%) will appear grayscale.

Lightness is the parameter which describes the scale from white to black of added light. A lightness of `100%` will always give you white.

To get true black, use `hsl(0 0% 0%)` or `(0deg 0% 0%)`.

Because the hue parameter is based on the color wheel, it takes a base of 0-360 degrees. You can also use the angle type, which is `0deg` or `0turn`. Both saturation and lightness are defined with percentages.

The [angle type](https://developer.mozilla.org/en-US/docs/Web/CSS/angle) is good for defining hue because it represents the angle of the color wheel well. It accepts degrees, turns, radians, and degrees.

Alpha is defined in `hsl()` like it is in `rgb()`. You can use `/` with `hsl` like `hsl(0 0% 0% / 50%)` or use `hsla()` like `hsla(0, 0%, 0%, 50%)`. Also like with `rgb`, you can use either a percentage or a decimal between 0 and 1.

### Other Color Types

`lab()` and `lch()`, which allow a wider range of color to be specified than is possible in RGB, are coming to CSS, but are not yet widely supported. Based on the MDN documentation, they are only available in Safari as of July 2021.

## Color Keywords

There are 148 named colors in CSS. MDN has the full list.

Aside from the standard colors, there are some special keywords.
`transparent` is a fully transparent color. It's the initial value of `background-color`.
`currentColor` is the contextual computed dynamic value of `color`, whatever it happens to be. If you have `color: red` and set `borderColor: currentColor`, the border will be red. If the element doesn't have a `color` value set, then `currentColor` will be computed by whatever the value of `color` from the cascade is.

System keywords are colors that are defined by your OS theme. Some examples of these colors are `Background`, the desktop background color, and `Highlight`, the highlight color of selected items. See [W3 wiki](https://www.w3.org/wiki/CSS/Properties/color/keywords#System_Colors) for the full list. Because color keywords are case insensitive, it's convention to capitalize SYSTEM COLORS to differentiate them from standard colors.

## Where to use color in CSS rules

If a CSS property accepts the `color` data type as a value, you can specify it using any of the above styles. For styling text, use `color`, `text-shadow`, and `text-decoration-color`. For backgrounds, set a color with `background` or `background-color`. You can also use colors in gradients, like `linear-gradient`. (Gradients get their own module later.) `border-color` and `outline-color` set the colors of borders and outlines. `box-shadow` also accepts color as a value.
