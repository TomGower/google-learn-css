# Functions

## What is a function?

(I know what functions are.) CSS functions are mostly pure functions. You can't write your own functions. You can nest functions in functions (`clamp(minmax)`).

## Functional selectors

We saw these in pseudo-classes, like `:is()` and `:not()`. E.g. `.post :is(h1, h2, h3)`.

## Custom properties and var()

`var()` is a function. It takes a custom property as an argument. Custom properties must be prefixed with `--`. Example:

```CSS
:root {
  --base-color: #ff00ff;
}

.my-element {
  background: var(--base-color);
}
```

You can pass a fallback declaration value into `var()`. E.g. `background: var(--base-color, hotpink)`. If `--base-color` is a valid value, it will be used; otherwise, the background will be hotpink.

## Functions that return a value

`var()` is an example. `attr()` and `url()` are others, and likewise are in the 'value' part of a CSS rule.

Example: `content: attr(href)`. `attr` is taking the value of the `<a>` element's `href` attribute and setting it as `content` (in their example, of an `::after` pseudo-element). This value will be updated dynamically as the value of `<a>`'s `href` changes.

Example: `background-image: url('/path/to/image.jpg')`. If the URL isn't valid or the resource isn't found, nothing will be returned by `url()`.

## Color functions

Covered in the Color Module, but you can define colors with some functions. E.g., `rgb()`, `rgba()`, `hsl()`, `hsla()`, `hwb()`, `lab()`, `lch()`. Pass in the right configuration arguments, get a color back.

## Mathematical expressions

**`calc()`**: takes a single mathematical expression as its parameter. The expression can be a mix of type, e.g. `width: calc(100% - 2rem)`. You can nest `calc()` instead a `calc()`, e.g. `calc(calc(10% + rem) * 2)`. `calc()` also accepts CSS variables, e.g. `calc(var(--root-height) * 3)`.

**`min()` & `max()`**: Do what their names suggest, return the smaller or larger of one or more passed arguments.

**`clamp()`**: takes three arguments: min, ideal, and max. E.g. `font-size: clamp(2rem, 1rem + 3vw, 3rem)`.

## Shapes

`clip-path`, `offset-path`, and `shape-outside` uses shapes to visually clip your box or provide a shape for content to flow around. Use shape functions like `circle()`, `ellipse()`, and `inset()` to size them. Or `polygon()`, which takes comma separated pairs of X and Y axis values to create custom shapes.

```CSS
.circle {
  clip-path: circle(50%);
}

.polygon {
  clip-path: polygon(0% 0%, 100% 0%, 100% 75%, 75% 75%, 75% 100%, 50% 75%, 0% 75%);
}
```

Similar to `polygon()`, `path()` takes an SVG fill rule as an argument. This allows for highly complex shapes that can be drawn in a graphics tool such as Illustrator or Inkscape and then copied into your CSS.

## Transforms

All of these functions are used with `transform`.

### Rotation

You can rotate an element using `rotate()`, which will rotate an element on its center axis. Alternatively, `rotateX()`, `rotateY()`, and `rotateZ()` to rotate on a specific axis. These functions accept degree, turn, and radian units for the level of rotation. Example:

```CSS
.my-element {
  transform: rotateX(10deg) rotateY(10deg) rotateZ(10deg);
}
```

`rotate3d()` takes four arguments. The first three numbers are the X, Y, and Z coordinates. The fourth is the rotation, and can be in degree, turn, or radian units. Example: `rotate3d(1, 1, 1, 10deg);`.

### Scale

`scale()` combined with `transform` lets you change the scaling of an element. It accepts one or two numbers as a value which determine a positive or negative scaling. With just one number argument, both X and Y axes will be scaled the same according to the shorthand value. Similar to `rotate()`, you can specify `scaleX()`, `scaleY()`, and `scaleZ()`. Example:

```CSS
.my-element {
  transform: scaleX(1.2) scaleY(1.2);
}
```

There is also a `scale3d()` function. It takes three arguments, the X, Y, and Z scale factors.

### Translate

`translate()` moves an element while it maintains its position in the document flow. It accepts length and percentage values as arguments. It translates an element along the X axis if one argument is passed, and translates an element along the X and Y axes if both arguments are passed. Example: `transform: translatex(40px) translatey(25px);`. (`translate()` = move).

Like `rotate()` and `scale()`, there is also `translateX()`, `translateY()`, and `translateZ()`, and also `translate3d()`, which accepts the X, Y, and Z as arguments in one function.

### Skewing

`skew()` lets you skew an element. It accepts angles as functions. It works similarly to `translate()`. It accepts one or two arguments. With one argument, it will only affect the X axis. With both arguments, the first value affects the X axis and the second the Y axis. `skewX()` and `skewY()` can be used if you only want to affect one axis. Example: `transform: skew(10deg);`.

### Perspective

`perspective()` will alter the distance between the user and the Z plane. This gives us the feeling of distance and can be used to create depth of field in your designs. (They have a supposedly cool design. My brain doesn't process it as 3D.)

### Animation functions, gradients, and filters

These each get their own module.
