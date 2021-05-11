# css

## selectors

[List of css selectors](https://www.w3schools.com/cssref/css_selectors.asp)
[List of css properties](https://css-tricks.com/almanac/properties/)

- `.class`
- `#id`
- `element`
- `[attribute]`

```css
selector {
    property: value;
    property2: values;
    /* mutiple values are separated by a space */
}

```
## Block Element Modifier BEM

[Overview](https://css-tricks.com/bem-101/)

TODO

## Tools

TODO: Icon, Color schemes etc...

## sass

- preprocessor for css
- .scss files
- more structured code through
  - variables
  - nesting
  - imports
  - mixins
  - functions

### import

You can import other scss files into the current one. The command `@import("mixin")` would import mixin.scss and add all variables and mixins into your file. if you import multiple files the order is kept.

### variables

You can define variables outside of a selector block and use them inside of one.

```scss
$variable_name=20px

.image {
    height: $variable_name
}

```

### nesting

With sass you do not need to nest the selectors inside each other if you want to address . Instead you can use the following syntax:

```scss
button {
    /* code */
}

img button {
    /* code which addresses all img Elements inside a button Element*/
}

```

### mixins

Mixins allow to define reusable code which can be used in selector blocks with @include:

```scss
@mixin boxmodel($radius) {
    padding: $radius;
    margin: $radius;
}

button {
    @include boxmodel(4px)
}

```

### functions and build-in modules

With @function ypu can define complex operations. @Use allows you to import build-in modules which contain mixins and functions. A list of the modules is given [here](https://sass-lang.com/documentation/modules)
