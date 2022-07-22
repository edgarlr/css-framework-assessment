# CSS Framework Assessment

## File Structure

```scss
pages
  |─  _app.js
  └─  index.js

styles
  |- main.scss
  |- tokens.scss // Tokens as CSS variables.
  |- base.scss
  |
  |- utilities
  |   |- _helpers.scss // Mixins for classes generation
  |   |- _theme.scss // Theme used on classes generation
  |   └─ typography.scss // Typography utility classes
  |
  |- components
        └─ header.scss

```

## CSS Variables

I decided to use CSS variables as tokens instead of SASS variables to keep all the advantages of the CSS custom properties. This helps to separate the token values from our theme so we can reuse any colors into borders, or reuse spacing tokens into margins and paddings, etc.

It also could make easy to add a dark theme by simply re-assigning our CSS custom properties without needing to update any part of the markup or theme. e.g.

```css
[data-theme="dark"] {
  --purple-50: #4c1d95; // --purple-900 hex in light theme
  --purple-100: #5b21b6; // --purple-800 hex in light theme
  //...
}
```

Similar to the dark theme, it allows us to update any text or spacing custom property in smaller devices. e.g.

```css
@media screen and (max-width: 425px) {
  --fontsize-sm: 15px; // 13px in bigger devices
  --fontsize-md: 17px; // 15px in bigger devices
  //...
}
```

## Exensibility

### Adding more text styles

After adding the new tokens for each text size, to auto generate all the new text utility classes it only requires to add each token under `$theme.typography`

```scss
typography: (
  // ...
  xs: (font-size: var(--fontsize-xl), line-height: var(--lineheight-xl))
);
```

### Adding more colors

After adding all new tokens, to auto generate all new utility classes for texts colors or any other utility classes using `generate-colors()`. It only requires to update the `$theme.colors`

```scss
colors: (
  // ...
  green: (50: var(--green-50), 100: var(--green-100), // ...)
);
```

### Adding more utility classes

To create a new utility class for background color we can reuse the `generate-colors()` and will create all new background color utility classes using the color pallet defined under `_theme.scss`.

```scss
.bg {
  @include generate-colors($attribute: "background-color");
}
```
