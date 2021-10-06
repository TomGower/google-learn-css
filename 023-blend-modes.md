# Blend Modes

Blend mode allows you to create compositional effects by mixing two or more layers, and lets you isolate an image with a white background.

Duotone is a popular color treatment for photography which makes an image look like it is only made up of two contrasting colors: one for highlights and the other for lowlights. Using blend modes—and other techniques you have learned about, such as filters and pseudo-elements—you can apply this effect to any image.

## What is a blend mode?

Blend modes are commonly used in design tools such as Photoshop to create a compositional effect by mixing colors from two or more layers. By changing how colors mix, you can achieve really interesting visual effects. You can also use blend modes as a utility, such as isolating an image that has a white background, so it appears to have a transparent background.

You can use most of the blend modes available in a design tool with CSS, using `mix-blend-mode` or `background-blend-mode` properties. `mix-blend-mode` applies to a whole element. `background-blend-mode` applies blending to the background of an element.

`background-blend-mode` can be used when you have multiple backgrounds on an element and want them all to blend into each other.

`mix-blend-mode` affects the entire element, including any pseudo elements. One use case is the initial example of a duotone image, which has color layers applied to the element through its pseudo elements.

Blend modes fall into two categories, separable and non-separable. A separable blend mode considers each color component, such as RGB, individually. A non-separable blend mode considers all color components equally.

## Separable blend modes

**Normal**: The default blend mode and changes nothing about how an element blends with others.

**Multiply**: Multiply blend mode is like stacking multiple transparencies on top of each other. White pixels will appear transparent, and black pixels will appear black. Anything in between will multiple its luminosity (light) values. Lights get much lighter and darks darker, most often producing a dark result. E.g. `mix-blend-mode: multiply`.

**Screen**: Using `screen` multiplies the light values, an inverse effect to `multiply`, and will most often produce a lighter result.

**Overlay**: Combines `multiply` and `screen`. Base dark colors become darker and base light colors become lighter. Mid-range colors, such as a 50% gray, are unaffected.

**Darken**: `darken` blend mode compares the source image and the background image's dark color luminosity, and selects the darker of the two. It does this comparing rgb values of luminosity (like `multiply` and `screen` would do) for each color channel. With `darken` and `lighten`, new color values are often created from this comparison process.

**Lighten**: `lighten` does the exact opposite of `darken`. (I assume it compares the source image and the background image, and selects the lighter of the two.)

**Color dodge**: If you use `color-dodge`, it lightens the background color to reflect the source color. Pure black colors see no effect from this mode.

**Color burn**: `color-burn` blend mode is very similar to `multiply` blend mode, but increases contrast, resulting in more saturated mid-tones and reduced highlights.

**Hard light**: Using `hard-light` creates a vivid contrast. This blend mode either screens or multiplies luminosity values. If the pixel value is lighter than 50% gray, the image is lightened, as if it were screened. If it's darker, it's multiplied.

**Soft light**: The `soft-light` blend mode is a less-harsh version of `overlay`. It works much the same way with less contrast.

**Difference**: A good way to picture how `difference` works is a bit like how a photo negative works. The `difference` blend mode takes the difference value of each pixel, inverting light colors. If the color values are identical, they become black. Differences in the values will invert.

**Exclusion**: Using `exclusion` is very similar to `difference`, but instead of returning black for identical pixels, it will return 50% gray, resulting in a softer output with less contrast.

## Non-separable blend modes

You can think of these blend modes like HSL color components. Each takes a specific component value from the active layer and mixes it with other component values.

**Hue**: The `hue` blend mode takes the hue of the source color and applies it to the saturation and luminosity of the backdrop color.

**Saturation**: `saturation` works like `hue`, but using `saturation` as the blend mode applies the saturation of the source color to the hue and luminosity of the backdrop color.

**Color**: The `color` blend mode will create a color from the hue and saturation of the source color and the luminosity of the backdrop color.

**Luminosity**: `luminosity` is the inverse of `color`. It creates a color with the luminosity of the source color and the hue and saturation of the backdrop color.

## The `isolation` property

If you set `isolation` to have a value of `isolate`, it will create a new stacking context, which will prevent it from blending with a backdrop layer. As covered in the z-index module, when you create a new stacking context, that layer becomes the base layer. This means that parent-level blend modes will no longer apply, but elements inside of an element with `isolation: isolate` set can still blend.

N.B. this doesn't work with `background-blend-mode` because the background property is already isolated.
