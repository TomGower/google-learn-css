# Animations

Animation is a way to highlight interactive elements and make things interesting and fun (for people who are into that sort of thing). Animations can be simple, one-state animations or complex, time-based sequences.

## What is a keyframe?

Keyframes are the mechanism that you use to assign animation states to timestamps, along a timeline.

In their example pulser animation, over 1 second, the animation runs over two states, dark circle to dark circle with light "halo" to dark circle. There's a specific point where each of these animation states start and end. You map these out with keyframes.

### `@keyframes`

Here's a basic `@keyframes` rule:

```CSS
@keyframes my-animation {
  from {
    transform: translateY(20px);
  }
  to {
  transform: translateY(0px);
  }
}
```

The `@keyframes` needs a name, which in this case is `my-animation`. The custom identifier works like a function name, allowing you to reference the rule elsewhere in your CSS. Identifiers are case-sensitive, and have some restricted words like `span`. (This appears to be wrong. Based on MDN (<https://developer.mozilla.org/en-US/docs/Web/CSS/custom-ident>), the forbidden values for animation names are the CSS global values of `unset`, `initial`, and `inherit`, plus `none`. Only CSS Grid appears to forbid `span`.)

`from` and `to` are shorthand for `0%` and `100%`, respectively. You can swap those in and out.

An animation can have as many positions as you like. Pulser looks like

```CSS
@keyframes pulse {
  0% {
    opacity: 0;
  }
  50% {
    transform: scale(1.4);
    opacity: 0.4;
  }
}
```

## The animation properties

To use your `@keyframes` in a CSS rule, define various animation properties or use the `animation` shorthand property.

### `animation-duration`

E.g., `animation-duration: 10s`. `animation-duration` defines how long the `@keyframes` timeline should be. It takes a time value, and defaults to 0 seconds. It does not accept negative time values.

### `animation-timing-function`

To help recreate natural motion, you can use timing functions that calculate the speed of animation at each step. If a value is calculated beyond that of the value defined in `@keyframes`, the animation may make the element appear to bounce.

Available preset values include `linear`, `ease`, `ease-in`, `ease-out`, and `ease-in-out`. These reference pre-defined bezier curves. You can also define your own bezier curve, e.g. `animation-timing-function: cubic-bezier(.42, 0, .58, 1)`.

If you want more granular control of your animation, you can use `steps()` to move in defined equal intervals instead. E.g., `animation-timing-function: steps(10, end)`.
The first argument is the number of steps. If the number of steps matches the number of keyframes (assume this is keyframe steps), each keyframe (step?) will play in sequence for the exact amount of time, with no transition between states. If there are not enough keyframes for the steps, steps between keyframes are added depending on the second argument.
The second argument to `steps()` is the direction. The default value is `end`. With that, the steps finish at the end of your timeline. If it's set to `start`, the first step of the animation completes as soon as it starts, which means it ends one step earlier than `end` (I don't think I understand what this means).

### `animation-iteration-count`

E.g., `animation-iteration-count: 10`. `animation-iteration-count` defines how many times `@keyframes` should run. Default value is 1, which means that when the animation reaches the end of its timeline, it will stop. Cannot be given a negative value. Can be `infinite`, which means the animation will loop.

### `animation-direction`

E.g. `animation-direction: reverse`. Allows you to set the direction the timeline runs over your keyframe. Default value is `normal` for forwards. `reverse` has the animation run backwards over the timeline. `alternate` means that for each animation iteration, the timeline will run forward or backward in sequence. `alternate-reverse` is the alternate version of reverse (so backwards then forwards, I guess).

### `animation-delay`

E.g., `animation-delay: 5s`. Defines how long to wait before starting the animation. Accepts a time value. This *can* be given a negative value. E.g, `@keyframe` is 10 seconds long and `animation-delays` is given `-5s`. In this case, the animation will start halfway through.

### `animation-play-state`

E.g., `animation-play-state: paused`. Allows you to pause and play the animation. Default value is `running`. If set to `paused`, the animation will be paused. (Their example is set `paused` on `:hover`, which seems like it would be the right use case.)

### `animation-fill-mode`

Defines which values in `@keyframes` timeline persist before the animation starts or after it ends. Default value is `none`, which means that when the animation is complete, the values in your timeline are discarded. Alternate values include `forwards`, in which case the last keyframe will persist based on the animation direction; `backwards`, in which case the first keyframe will persist based on the animation direction; and `both`, which follows the rules for the both `forwards` and `backwards`. (Their visual example doesn't do a good job of letting me see the difference between `forwards` and `backwards`, and I have no idea how `both` works.)

### The `animation` shorthand

Instead of defining all the properties separately with their name, you can define them in an `animation` shorthand. This accepts the properties in the order `animation-name`, `animation-duration`, `animation-timing-function`, `animation-delay`, `animation-iteration-count`, `animation-direction`, `animation-fill-mode`, and `animation-play-state`. Example usage

```CSS
.my-element {
  animation: my-animation 10s ease-in-out 1s infinite forwards forwards running;
}
```

## Considerations when working with animation

Users can define in their OS when they prefer to reduce motion experienced when they interact with applications and websites. Check this with `prefers-reduced-motion` media query.

```CSS
@media (prefers-reduced-motion) {
  .my-autoplaying-animation {
    animation-play-state: paused;
  }
}
```
