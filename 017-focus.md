# Focus

When a skip link is activated with tab or enter, the target of the skip (`main` in their example) has a focus ring around it. This is because `main` has a `tabindex="-1"` attribute value, which means it can be programmatically focused. When `main` is targeted - because `#main-content` in the URL matches the `id` - it receives programmatic focus. Handling focus appropriately and with care helps to create a good, accessible user experience. It can also be a good place to add some interest to interactions.

## Why is focus important?

Creating accessible focus states with CSS is part of the job as a web dev of making a website accessible and inclusive to all.

## How elements get focus

Certain elements are automatically focusable. These are elements that accept interaction and input, such as `<a>`, `<button>`, `<input>`, and `<select>`. So, form elements, buttons, and links. You can typically navigate a page's focusable elements using `tab` to go forward and `shift+tab` to go backwards.

There is the HTML attribute `tabindex` which allows you to change the tabbing index—which is order in which elements are focused—every time someone presses their tab key, or focus is shifted with a hash change in the URL or by a JavaScript event. If `tabindex` on a HTML element is set to 0, it can receive focus via the tab key and it will honour the global tab index, which is defined by the document source order. (copypasta, not quite sure I get all of this enough to express in my own words)

If you set `tabindex="-1"`, it can only receive focus programmatically, which means only when a JS event occurs or a hash change (URL matching element's `id`). If you set `tabindex` higher than 0, it will be removed from global tab index, defined by the DOM. Tabbing order will then be defined by the value of `tabindex`, so an element with `tabindex="1"` will receive focus before an element with `tabindex="2"`.

N.B. modifying `tabindex` is like Flexbox and Grid and you should change it relative to DOM order if you absolutely have to change it. Anything that creates unpredictable focus on the web can create an inaccesisble experience for the user.

## Styling focus

Default browser behavior is to present a focus ring when an element receives focus. The look of the focus ring differs between browsers.

Browser focus look can be changed with CSS, using `:focus:`, `:focus-within`, and `:focus-visible` as seen in the pseudo-classes module.
N.B. focus should have *contrast* with the default style of an element. Common approach: use the outline property, like:

```CSS
a:focus {
  outline: 2px solid slateblue;
}
```

`outline` might appear too close to the text of a link. `outline-offset` can help with that, adding extra visual padding without affecting the geometric size that the element fills. A positive number for `outline-offset` will push the outline outwards, and a negative value will pull the outline inwards.

```CSS
a:focus {
  outline: 2px solid slateblue;
  outline-offset: 6px;
}
```

Relative to the prior example, the outline is further set apart from the text of the link.

Currently, in some browsers, if you have `border-radius` set on an element and use `outline`, it won't match. The outline will have sharp corners. You may want to try to fix this with `box-shadow` with a small blur radius because `box-shadow` clips to its shape, honoring `border-radius`. But this style will not show in Windows High Contrast Mode, because WHCM doesn't apply shadows and mostly ignores background images to favor the user's preferred settings.

## Summary

Default browser styles contrast with an element's default state. If you want to change this behavior, note a few things:

-Avoid using `outline: none` on an element that can receive keyboard focus
-Avoid replacing `outline` styles with `box-shadow` as they don't show up in Windows High Contrast Mode
-Only set a positive value for `tabindex` on an HTML element if you absolutely have to
-Make sure the focus state is very clear relative to the default state
