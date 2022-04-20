# SCSS Breakpoint Classes

[_SCSS_](https://sass-lang.com/) mixin used to generate breakpoint specific classes following the name structure `.selector:[BREAKPOINT]` from selectors. It also supports filter to only include specific breakpoints for each selector to reduce the CSS size.

## Usage

Add the folder `breakpoint-classes` to your _SCSS_ project and import `breakpoint-classes` using `@use`.

```scss
@use "breakpoint-classes" as *;

.foo {
  @include breakpoint-classes {
    /* Styling */
  }
}
```

The example above will genereate breakpoint specific classes for all breakpoints found in `$breakpoints` in `breakpoint-classes/_breakpoint-classes.scss`. The output will look like this:

```css
.foo {
  /* Styling */
}

@media (min-width: 600px) {
  :is(.foo\:sm, #breakpoint-important) {
    /* Styling */
  }
}

@media (max-width: 599px) {
  :is(.foo\:lt-sm, #breakpoint-important) {
    /* Styling */
  }
}

/* ...and so on for each breakpoint */
```

> The mixin uses `:is()` with the id selector `#breakpoint-important` to increase its specificity.

The mixin uses escaped ":" character to build the class names. Below is an example on how to use the `.foo` styling in the breakpoint **sm**.

```html
<div class="foo:sm">
  <!-- Content -->
</div>
```

### Filter

The `breakpoint-classes` mixin takes `$filter` as a _SCSS_ list to configure what breakpoints to include. By default all breakpoints in `$breakpoints` are included.

```scss
@use "breakpoint-classes" as *;

$foo-filter: (md, lt-md);

.foo {
  @include breakpoint-classes($foo-filter) {
    /* Styling */
  }
}
```

The example above will only generate breakpoint specific classes for the breakpoints **md** and **lt-md**.

## Work in this repository

Before you start working in this repository, install the dependencies.

```bash
npm install
```

### Compile SCSS to CSS

This repository includes a demo file to test the mixin found in `demo/demo.scss`. Compile the demo _SCSS_ into CSS by running the following command.

```bash
npm run sass
```

The scripts will output a CSS file at `dist/demo.css`.

### Code formatting

This project uses [Prettier](https://prettier.io/) to format the code. To format all files, run the following command.

```bash
npm run prettier
```

### Lint

This project uses [Stylelint](https://stylelint.io) to lint the _SCSS_. The settings is based on `stylelint-config-standard-scss`. To run the lint, run the following command.

```bash
npm run stylelint
```
