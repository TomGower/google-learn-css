# The Cascade

CSS = Cascading StyleSheets. The cascade is the algorithm for solving conflicts when multiple CSS rules apply to an HTML element.

```CSS
button {
  color: red;
}

button {
  color: blue;
}
```

With the above CSS, `button`'s text will be `blue`.

The cascade algorithm is split into four different stages: position and order of appearance, specificity (which selector has the strongest match), origin of CSS (order of multiple stylesheets and where it comes from, browser style, browser extension, your own), and importance (`!important`).

## Position and order of importance

The demo above is a straightforward example of this. There are two rules with identical specificty, so the last to be declared won.

If you have a `<link>` that includes CSS at the top of your HTML page and another `<link>` that includes CSS at the bottom of your page, the bottom `<link>` will have the most specifity so its styles will "win" (my word). `<style>` elements work the same way-the ones at the bottom of the page are more specific.

An inline style attribute with CSS declared in it will override all CSS, regardless of position, unless it is `!important`.

Position also matters within your CSS rule.

```CSS
button {
  color: red;
  color: blue;
}
```

In the above CSS, `button`'s text will be `blue`.

This is particularly useful as a simple way to create fallbacks for browsers that do not support a particular value.

```CSS
.my-element {
  font-size: 1.5rem;
  font-size: clamp(1.5rem, calc(1rem + 3vw), 2rem);
}
```

If the browser does not support `clamp()`, the second declaration will be ignored and the first will be applied. If the browser does support `clamp()`, the second declaration will be applied.

## Specificity

By making a rule more specific, you can cause it to be applied even if some other CSS that matches the selector appears later in the CSS.

CSS targeting on a class will make that rule more specific, and therefore seen as more important to be applied, than CSS targeting the element alone. Example:

```HTML
<style>
  .my-element {
    color: red;
  }
  h1 {
    color: blue;
  }
</style>
<h1 class="my-element">Heading</h1>
```

In the above example, "Heading" will be `red` because `.my-element` has greater specificity than `h1` even though it appears first.

An `id` makes the CSS even more specific, so styles applied to with `#id` will override those applied many other ways. This is one reason why it is generally not a good idea to attach styles to `#id`, because it makes it hard to override.

Specificity is also cumulative, which makes it hard to override very detailed and specific selectors. This is one reason why it's a good idea to keep your selectors as simple as possible, because doing it otherwise makes it hard to override.

Specificity will be covered in more detail in a later module.

## Origin

The cascade takes into account the origin of the CSS. The order of specificity of those settings is as follows:

1. User agent base styles. The styles the browser applies to HTML by default.
2. Local user styles. These come from the operating system, like base font size or preference for reduced motion. This also includes browser extensions, like those that allow a user to write their own CSS for a webpage.
3. Authored CSS. The CSS that you author.
4. Authored `!important`. Any `!important` that you add to your authored declarations.
5. Local user styles `!important`. Any `!important` that comes from the operating system level, or browser extension level CSS.
6. User agent `!important`. Any `!important` that are defined in the default CSS, provided by the browser.

## Importance

Not all CSS rules are calculated the same, or are given the same specificity. The order of importance, from least to most, is as follows:

1. Normal rules, such as `font-size`, `background`, or `color`
2. `animation` rule type
3. `!important` rule type (in the same order as Origin)
4. `transition` rule type

Active animation and transition rule types have higher importance than normal rules. In the case of transitions, they have even higher importance than `!important` rule types. This is because when an animation or transition becomes active, its expected behaviour is to change visual state.

## Summary

The Cascade can:

-Resolve conflicts when multiple styles apply to an element
-Ensure there's only one style value for each property at draw time
-Score and weight style rules
-Sort and filter style attributes (as part of conflict resolution)
