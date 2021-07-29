# Flexbox

Flexbox solves single-dimension layout problems. (I'm simplifying. I've worked on Flexbox before.)

## What can you do with a flex layout?

Display as row or column.
Respect the writing mode of the document.
Single line by default, but can wrap on multiple lines.
Items in the layout can be visually reordered, away from their DOM order.
Space can be distributed inside the items, so they become bigger or smaller based on the size of the parent.
Space can be distributed around the items and flex lines in a wrapped layout.
The items can be aligned on the cross axis.

## The main axis and the cross axis

Flexbox always has a main axis and a cross axis. Items move as a group on the main axis. Set main axis with `flex-direction`.

## Creating a Flex container

Set `display: flex` on the parent. This makes the parent a block-level box, as noted in Module 8. Default behavior:

Items display as a row.
Items do not wrap.
Items do not grow to fill the container.
Items line up at the start of the container.

## Controlling the direction of items

`flex-direction` sets the direction of the alignment of the Flex children (my language). `row` is default. Also `row-reverse`, `column`, `column-reverse`.

### Reversing the flow of items and accessibility

Be cautious using any properties that reorder the visual display of items from their DOM order. `row-reverse` and `column-reverse` are good examples of this. Their video example is similar to the simple one: 1-2-3-4 in DOM order, 4-3-2-1 displayed using `row-reverse`, user gets 1-2-3-4, so navigates the visual display "backwards."

### Writing modes and direction

The default direction of `row` is the direction of the browser. English, left-to-right. Arabic, right-to-left. Vertical writing modes, top-to-bottom.

For that reason, Flexbox works with `start` and `end` rather than `top`, `right`, `bottom`, and `left`. In a row in English `main-start` is left. In a column, it would be top. Similarly, `main-end` is right for row in English and bottom in a column. `cross-start` and `cross-end` operate similarly on the other axis (left/right in column, top/bottom in row in English).

## Wrapping flex items

The default value of `flex-wrap` is `nowrap`. This creates overflow if the Flex container is not wide enough to contain its children even after the children have shrunk to `min-content`.

When a Flex container wraps, it creates multiple *flex lines*. Each flex line acts like a new container. If you're wrapping rows, you can't get something in row 2 to line up to something above it in row 1.

### The flex-flow shorthand

`flex-flow` lets you set `flex-direction` and `flex-wrap`. Example: `flex-flow: column wrap`.

## Controlling space inside flex items

If the container has more space than the items require, by default the items line up at the start and do not grow to fill the space. They space growing at max-content.

Default values:
`flex-grow: 0`-items do not grow
`flex-shrink: 1`-items can shrink smaller than their `flex-basis`
`flex-basis: auto`-items have a base size of `auto`
Shorthand for this is `flex: initial`.

Alternatively, `flex: auto`:
`flex-grow: 1`-items can grow larger than their `flex-basis`
`flex-shrink: 1`-items can shrink smaller than their `flex-basis`
`flex-basis: auto`-items have a base size of `auto`

Using `flex: auto`, items will end up different sizes, as space is shared between items after each item is laid out at `max-content` size.

Alternatively, `flex: 1`:
`flex-grow: 1`-items can throw larger than their `flex-basis`
`flex-shrink: 1`-items can shrink smaller than their `flex-basis`
`flex-basis: 0`-items have a base size of `0`.
All items have an equal size, therefore all of the space in the flex container is available to be distributed.

### Allowing items to grow at different rates

You can give individual flex children their own `flex-grow` property so that not all children of a Flex container expand at the same rate. Example:

```CSS
.item1 {
  flex: 1 1 auto;
}

.item2 {
  flex: 2 1 auto;
}
```

## Reordering flex items

Items in your flex container can be reordered using the `order` property. This allows the reordering in *ordinal groups*. Items are laid out in their direction set by `flex-direction`, with lowest values first. If more than one item has the same value, it will be displayed with the other items with that value.

N.B. `order` has the same accessibility issues as `row-reverse` and `column-reverse`, with items being visually displayed outside of their DOM/tab order.

## Flexbox alignment overview

Flexbox has properties for aligning items and distributing space between items. But they're so useful they've been moved out of the Flexbox specification because they're used in Grid too. This will discuss how they work in Flexbox.

The set of properties can be placed into two groups, properties for space distribution and properties for alignment.

Space distribution properties:
`justify-content`: space distribution on the main axis
`align-content`: space distribution on the cross axis
`place-content`: shorthand for setting both of the above two

Alignment properties:
`align-self`: aligns a single item on the cross axis
`align-items`: aligns all of the items as a group on the cross axis

Basic rule:
main axis: `justify-`
cross axis: `align-`

## Distributing space on the main axis

Initial value of `justify-content` is `flex-start`. Items line up at the front, extra space is at the end.

Alternate value: `flex-end`. Items line up at the back, extra space is at the front.

Alternate value: `space-between`. Items get space between them. First item is at front, last item is at end.

Alternate value: `center`. Items are centered.

Alternate value: `space-around`. Items get space between them. This includes space at front before first item and item at end after last item.

Alternate value: `space-evenly`. (More or less, each child gets a column of equal width.)

If you don't have spare space on the main axis, `justify-content` won't do anything.

### With `flex-direction: column`

To have spare space in your container when working as a column, you need to give the container a `height` or `block-size`. Otherwise you won't have spare space to distribute.

## Distributing space between flex lines

With a wrapped flex container you might have space to distribute on the cross axis. In that case, you can use `align-content` with the same values we just saw for `justify-content`.

The default value of `align-content` is `stretch` and not `flex-start`.

### The `place-content` shorthand

You can set both `justify-content` and `align-content` with `place-content`. If you give one value, it will be assigned to both axes. If you give two values, and the first will be for `align-content` and the second for `justify-content`.

Example #1: `place-content: space-between`. Sets both `justify-content` and `align-content` to `space-between`.
Example #2: `place-content: center flex-end`. Sets `align-content: center` and `justify-content: flex-end`.

## Aligning items on the cross axis

On the cross axis, you can also align items within the flex line using `align-items` and `align-self`. The space depends on the height of the flex container, or the flex line in the case of wrapped line items.

The initial value of `align-self` is `stretch`. Items in a flex row stretch to the height of the tallest item. You can change this for individual children with `align-self` on a Flex child.

Possible values are `flex-start`, `flex-end`, `center`, `stretch`, and `baseline`.

## Why is there no `justify-self` in flexbox?

Flex items act as a group on the main axis. There is no concept of splitting an individual item out of the group (which is how you end up with nested Flex containers).

In grid, `justify-self` and `justify-items` work on the inline axis to affect alignment of items on that axis within their grid area.

Flexbox does work nicely with auto margins. If you come across a need to split off one item from a group, or separate the group into two groups you can apply a margin to do this. In the example below the last item has a left margin of `auto`. The auto margin absorbs all space in the direction it is applied. This means that it pushes the item over to the right, thus splitting the groups.

## How to center an item vertically and horizontally

`display: flex; justify-content: center; align-items: center`.

In the future, we may be able to do this without making the parent a flex container. At present, no browser supports this. Switching to a flex context gives you axis to these properties, so is a great way to align stuff (very paraphrased).
