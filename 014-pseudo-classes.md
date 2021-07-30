# Pseudo-classes

Pseudo-classes let you apply CSS based on state changes. Example: email sign up form, email form field should get a red border if the user supplies an invalid email address. This can be done with the `::invalid` CSS pseudo-class, one of many browser-provided pseudo-classes.

Whereas pseudo-elements let you style parts of an element, pseudo-classes let you style an element based on the specific state it might be in.

## Interactive states

These are pseudo-classes that apply due to an interaction a user has on the page.

`::hover` applies an effect when a user with a pointing device puts their pointer over the element.

`::active` is triggered when an element is actively being interacted with, such as a click, and before the click is released.

`::focus`, `:focus-within`, and `:focus-visible`. If an element can receive focus, e.g. `<button>`, you can apply styling to that element with `::focus`. You can apply styling if a child element of your element receives focus with `:focus-within`. Focusable elements like `<button>` will show a focus ring when they are in focus, even when clicked. You can remove that with `button:focus {outline: none;}`. That CSS removes the default browser focus ring when an element receives, focus, which presents an accessibility issue related to keyboard navigation. If there is no focus style, keyboard users cannot keep track of where focus is when using `tab`. With `:focus-visible`, you can apply focus styling, while also using `outline: none` to prevent it when a pointer is used. Pair with `button:focus-visible {outline: 1px solid black;}`.

`:target` selects an element that has an `id` matching a URL fragment. Imagine this:

```HTML
<article id="content">
  …
</article>
```

You can attach styles to that element when the URL contains `#content`.

```CSS
#content:target {
  background: yellow;
}
```

This is helpful for highlighting areas that have been specifically linked to, like specific content, via a skip link.

## Historic states

### `:link`

`:link` can be applied to any `<a>` with an `href` value that has not yet been visited.

You can use `:visited` to style a link that's already been visited. For security reasons, you can use fewer CSS properties here. You can only use `color`, `background-color`, `border-color`, `outline-color`, and the color of SVG `fill` and `stroke`.

N.B. if you define a `:visited` style, it can be overridden by a link pseudo-class with at least equal specificity. So you should use the LVHA rule for styling links with pseudo-classes in a particular order: `:link`, `:visited`, `:hover`, `:active`.

## Form states

### `:disabled` and `:enabled`

If a form element is disabled by the browser, you can style it with `:disabled`. You can use `:enabled` to style the opposite state, but because this is the default state for form elements, you might not use it very much.

### `:checked` and `:indeterminate`

`:checked` will style a checkbox when it has been checked.

`:indeterminate` will style a checkbox when it has not been checked nor unchecked. The example is when you have a "select all" control that controls all of the checkboxes in a group. When just one of the checkboxes in the group is checked, the root checkbox would no longer represent all being checked, so should be put into an indeterminate state.

Another use case is the `<progress>` element, and giving it a striped appearance to indicate it's unknown how much more is needed.

### `:placeholder-shown`

If a form field has `placeholder` and no value, `:placeholder-shown` can be used to style specifically that state. As soon as there is content in the field, whether `placeholder` or not, this styling will no longer apply.

### Validation states

You can respond to HTML form validation with pseudo-classes like `:valid`, `:invalid`, and `:in-range`. `:valid` and `:invalid` can be helpful for showing the user the correct values for a form field that must match a particular pattern like an email input.

`:in-range` is available if the input has a `min` and `max`, such as a numeric input, and the value is within those bounds.

You can use `:required` to style fields that are required, and `:optional` to style fields that are not required.

N.B. it's not a good idea to rely solely on color to signify state changes-especially red and green-because colorblind and low-vision users can struggle to see a state change, or even miss it completely. A good idea is to use color to support state changes, along with text changes and icon changes to visually signify change.

## Selecting elements by their index, order, and occurrence

`:first-child` and `:last-child` will return the first or last element in a group of sibling elements.

`:only-child` will select elements with no siblings, like the list item in a list with only one item.

`:first-of-type` and `:last-of-type` might seem the same as `:first-child` and `:last-child`, but can be selectively applied to elements of a particular type. Imagine `<div class="parent">` with `<h2><div><div>` inside it. You can use `.parent div:first-of-type` to target the first paragraph. Using `.parent div:first-child` not not target anything, because `:first-child` is a `<h2>`

`:nth-child()` and `:nth-of-type()` let you select an element other than the first or last. CSS indexing starts at 1. `odd` and `even` are both permitted values. Also `An + B`, where the initial value of `n` is `0`.

`:only-of-type` lets you select the only element of a certain type in a group. This is useful for lists with only one item, or if you want to find the only `<strong>` element in a paragraph.

## Finding empty elements

`:empty` will select elements with no children. Children includes HTML elements, text nodes, **and** whitespace, so `<div>  </div>` would not be selected by `:empty`.

`:empty` can be useful if you have little control over the HTML and want to hide empty elements, such as a WYSIWYG content editor. Example:

```HTML
<article class="post">
 <p>Donec ullamcorper nulla non metus auctor fringilla.</p>
 <p></p>
 <p>Curabitur blandit tempus porttitor.</p>
</article>
```

Hide the empty `<p>` with `.post :empty { display: none; }`.

## Finding and excluding multiple elements

One option for selectors: `.post h2, .post li, .post img {...}`.
Another way to do the same thing: `.post :is(h2, li, img) {...}`.

`:is()` is more compact than a selector list. It is also more forgiving. If there's an error or unsupported selector in a selector list, the entire selector list will no longer work. If there's an error in `:is()`, it will ignore the invalid selector but use those which are valid.

`:not()` lets you exclude items. Example: style all links that don't have a `class` attribute with `a:not([class])`. Example #2: style all `<img>` that don't have an `alt` attribute for accessibility with `img:not([alt])`.
