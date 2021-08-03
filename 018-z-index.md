# Z-index and stacking contexts

When absolutely positioned elements are in the same position, which is displayed on top of the other? z-index and stacking contexts answer that question.

## Z-index

`z-index` explicitly sets an order layer for HTML elements based on the Z (third-dimensional) axis. The vertical axis on web is the Y axis and the horizontal axis is the X axis.

`z-index` accepts a numerical value, which can be a positive or negative number. Elements with the higher `z-index` are displayed on top. With no `z-index` set, DOM order dictates the Z axis.

`z-index` will have no effect if the element is set to `position: static` or otherwise is not given a `position` property. Exception: Flexbox and Grid create their own stacking context

## Negative z-index

You can set a negative `z-index` to position one element behind another element. Example:

```CSS
.my-element {
  background: rgb(232 240 254 / 0.4);
}

.my-element .child {
  position: relative;
  z-index: -1;
}
```

`.child` sits behind `.my-element` in the above example. But you can change that:

```CSS
.my-element {
  position: relative;
  z-index: 0;
  background: rgb(232 240 254 / 0.4);
}
```

`.my-element` now has a `position` that's not static and `z-index` value that's not `auto`. It has therefore created a new *stacking context*. This means even if you set `.child` to have a very low z-index value, it would still not sit behind `.my-element`.

## Stacking context

A *stacking context* is a group of elements that have a common parent and move up and down the z-axis together.

Example: `parent1` has `z-index: 1`. `childOfParent1` has `z-index: 999`. `parent2` is a sibling of `parent1` and `z-index: 2`. `childOfParent2` has `z-index: 2`. The element rendered on top is `childOfParent2`. Even though its `z-index` is less than that of `childOfParent1`, both parents create a stacking context and the `z-index` of the children is based on that of their respective parent. Consequently, the two children are rendered relative to their parent's current order in its own stacking context.

N.B. the `<html>` element is a stacking context and no element can ever go behind it. You can put stuff behind `<body>` until you create a stacking context with it.

## Creating a stacking context

Adding a `z-index` and `position` are not the only ways to create a stacking context. You can create a new stacking context by adding a value for properties that create a new composite layer, such as `opacity`, `will-change`, or `transform`. See [MDN](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_Positioning/Understanding_z_index/The_stacking_context) for the full list of ways to create a stacking context.
