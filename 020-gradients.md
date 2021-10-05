# Gradients

Imagine there's an image with a background featuring a purple background with two different shades of purple turning into each other. You might think it requires an image from your design tool to do this, but you can use `linear-gradient` instead.

A gradient is an image and can be used anywhere images can be used, but it's created with CSS and is made up with colors, numbers and angles. CSS gradients allow you to create anything from a smooth gradient between two colors, right up to impressive artwork by mixing and repeating multiple gradients.

## Linear gradient

`linear-gradient()` generates an image of two or more colors, progressively. It takes multiple arguments. In its simplest form, you can pass some colors like `background: linear-gradient(black, white);` and it will automatically split them evenly, while blending them.

You can also pass an angle or keywords that represent an angle. if you use keywords, specify the direction after `to`. `background: linear-gradient(to right, black, white);` produces a background that goes from black on the left to white on the right.

A color stop value defines where a color stops and mixes with its neighbors. `background: linear-gradient(45deg, darkred 30%, crimson);` defines a gradient staring with a dark shade of red running at a 45% degree angle, and at 30% of the size of the gradient changing to a lighter red.

`linear-gradient()` accepts as many colors and color stops as you want to give it, and you can layer gradients on top of each other by separating each gradient with a comma. (Josh was MUCH better at explaining this, and much more explicit about the meaning of the values and how to do real color stops.)

## Radial gradient

`radial-gradient()` lets you create a gradient that radiates in a circular fashion. Instead of specifying an angle like in `linear-gradient()`, you optionally specify a position and an ending shape. If you just specify colors, `radial-gradient()` will have a default position of `center` and select either a circle or ellipse, depending on the size of the box.

The gradient's position is similar to `background-position` using keywords and/or number values. The size of the radial gradient determines the size of the gradient's ending shape (circle or ellipse) and by default will be `farthest-corner`, which means it exactly meets the farthest corner of the box from the center. You can also use `closest-corner`, to specify the closest corner to the center of the gradient; `closest-side`, which will meet the side of the box closest to the center of the gradient, and `farthest-side`, which will meet the side of the box farthest from the center of the gradient.

Like `linear-gradient()`, you can add as many color stops as you like. Likewise, you can have as many `radial-gradients()` as you want.

## Conic gradient

A conic gradient has a center point in the element and starts from the top by default, going around in a 360 degree circle. `background: conic-gradient(white, black)` produces a gradient that goes from white to black from the right to left side of the "clock-like box".

`conic-gradient()` accepts position and angle arguments.
The default angle is 0 degrees. If you set the angle to `45deg` the gradient starts in the top right corner. It accepts any angle value, like linear and radial gradients.
The default position is center. Like linear and radial gradients, positioning can be keyword-based or defined with numeric values.

You can add as many color stops as you want. A good use for this capability is pie charts.

```CSS
.my-element{
  background: conic-gradient(
    gold 20deg, lightcoral 20deg 190deg, mediumturquoise 190deg 220deg, plum 220deg 320deg, steelblue 320deg
  );
}
```

## Repeating and mixing

Each type of gradient also has a repeating type. These are `repeating-linear-gradient()`, `repeating-conic-gradient()`, `repeating-radial-gradient()`. They take the same arguments as the non-repeating functions. If the defined gradient can be repeated to fill the box, based on both the size of the gradient and the size of the box, it will.

If the gradient doesn't appear to be repeating, you probably haven't set a length for one of the color stops. For example, create a striped background with:

```CSS
.my-element {
  background: repeating-linear-gradient(
    45deg,
    red,
    red 30px,
    white 30px,
    white 60px
  );
}
```

You can mix multiple gradients together, whether they're the same gradient type or different types.

```CSS
.my-element {
  background: linear-gradient(-45deg, blue -30%, transparent 80%), linear-gradient(45deg, darkred 20%, crimson, darkorange 60%, gold, bisque);
}
```
