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
