# Fylgja - FontFace

[![Fylgja Package](https://img.shields.io/badge/Fylgja-Package-blue.svg?style=flat-square)](https://github.com/topics/fylgja-package)
![Version](https://img.shields.io/badge/version-v1.2.0-green.svg?style=flat-square)

The Fylgja font-face mixin makes it super easy to load fonts.
It will set all required settings for a good font-face automatically.
Which are still configurable if needed.

## How to use

First git clone or download the repo to you're project.
```bash
$ git clone git@github.com:WS-Concepts/fylgja-fontface.git
```

Include the font-face package in to your code.

```scss
@import "fylgja-fontface/lib";
```

To load a font.
Call the font-face mixin.
Add your font name + suffix of the font.

_All the other steps will be created by the mixin automatically (See [config](#config))._

```scss
@include font-face('Roboto', 'Regular');
@include font-face('Roboto', 'Bold Italic');
```

```css
@font-face {
  font-family: "Roboto";
  src:
    local("Roboto"),
    local("Roboto-Regular"),
    url("../fonts/Roboto-Regular.woff2") format("woff2"),
    url("../fonts/Roboto-Regular.woff") format("woff");
  unicode-range: "U+0000—00FF";
  font-weight: 400;
  font-style: normal;
  font-display: swap;
}

@font-face {
  font-family: "Roboto";
  src:
    local("Roboto Bold Italic"),
    local("Roboto-BoldItalic"),
    url("../fonts/Roboto-BoldItalic.woff2") format("woff2"),
    url("../fonts/Roboto-BoldItalic.woff") format("woff");
  unicode-range: "U+0000—00FF";
  font-weight: 700;
  font-style: italic;
  font-display: swap;
}
```

## Config

There is no real config except the mixin options that you can pass per font.

Most options are filled in.
_if left to its default value._

For this reason it is better to call a specific option. Instead changing the complete mixin options until you've reached the option you need to change.

**Examples;**

Bad way:
```scss
@include font-face('Roboto', 'Regular', 400, $u-latin, '../assets');
```

Good way:
```scss
@include font-face('Roboto', 'Regular', $path: '../assets');
```

Options      | Default value      | Description
-------------|--------------------|-------------
`$name`      |                    | The name of the font.
`$suffix`    | _null_             | The suffix of the font (example: Bold).
`$styles`    | $suffix            | The styles (weight/style) of the font. The value will be set automatically via the suffix name if not set. The styles also allows values like `400i`. Which is the same as 400 Italic.
`$unicode`   | $u-latin           | The unicode range of the the font face.
`$path`      | '../fonts'         | The path to the font file
`$file-name` | _null_             | The file name of the font. The value will be set automatically via the name + suffix if not set.
`$formats`   | local, woff2, woff | The file formats of the font-face.
`$load`      | swap               | The loading option of the font ([See the Mozila Doc for more info](https://developer.mozilla.org/en-US/docs/Web/CSS/@font-face/font-display))

_If an option is missing. Plz leave a feature request._

## Tips

### Loop

You can load the entire Roboto font stack via a foreach loop.

```scss
$fonts-roboto: (
    'Light',
    'Light Italic',
    'Regular',
    'Italic',
    'Bold'
);

@each $styles in $fonts-roboto {
    @include font-face('Roboto', $styles);
}
```

### Icons

You can use this mixin to also load font icon libraries.
Simply call the mixin as describe above but leave the suffix field to its default value of _null_

```SCSS
@include font-face('FontAwesome', $unicode: $u-all);
```

Or use the suffix value of `'Regular'`

```scss
@include font-face('Material Icons', 'Regular', $unicode: $u-all);
```

This will set by default the:
* font-weight to 400
* font-style to normal

You must still set the `$unicode`, since icon libraries have diffrent ones than Latin.
