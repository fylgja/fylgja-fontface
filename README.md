# Fylgja - font-face

![Fylgja Package](https://img.shields.io/badge/Fylgja_Package-Font--Face-blue.svg?style=flat-square)

This package is not part of the [core framework](https://github.com/GrimLink/fylgja) and can be used without it.

## Why use this

The font-face mixin makes it super easy to load fonts.
It will set all required settings for a good font-face automatically.
Which are still configurable if needed.

## How to use

First git clone or download the repo to you're project.
```bash
$ git clone git@github.com:GrimLink/fylgja-font-face.git
```

Include the font-face package in to your code.

```SCSS
@import "fylgja-font-face/font-face";
```

And to load a font.
Call the font-face mixin.
And add your font name + suffix of the font type.

_All the other steps will be created by the mixin automatically (See [config](#config))._

```SCSS
@include font-face('Roboto', 'Regular');
@include font-face('Roboto', 'Bold Italic');
```

```CSS
@font-face {
  font-family: "Roboto";
  src: local("Roboto"), local("Roboto-Regular"),
       url("../fonts/Roboto-Regular.woff2") format("woff2"),
       url("../fonts/Roboto-Regular.woff") format("woff");
  unicode-range: "U+0000—00FF";
  font-weight: 400;
  font-style: normal;
  font-display: swap;
}
@font-face {
  font-family: "Roboto";
  src: local("Roboto Bold Italic"), local("Roboto-BoldItalic"),
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

Most options are filled in, if left to its default value.

For this reason it is better to call a specific option instead of changing the complete mixin options until you've reached the option you need to change.

**Bad way:** `@include font-face('Roboto', 'Regular', 400, $u-latin, '../assets');`

**Good way:** `@include font-face('Roboto', 'Regular', $path: '../assets');`

Options      | Default value      | Description
-------------|--------------------|-------------
`$name`      |                    | The name of the font.
`$suffix`    | _null_             | The suffix of the font (example: Bold).
`$variant`   | $suffix            | The variant (weight/style) of the font. The value will be set automatically via the suffix name if not set. The variant also allows values like `400i`. Which is the same as 400 Italic.
`$unicode`   | $u-latin           | The unicode range of the the font face. Default is the latin range.
`$path`      | '../fonts'         | The path to the font file
`$file-name` | _null_             | The file name of the font. The value will be set automatically via the name + suffix if not set.
`$formats`   | local, woff2, woff | The file formats of the font-face.
`$load`      | swap               | The loading option of the font ([See the Mozila Doc for more info](https://developer.mozilla.org/en-US/docs/Web/CSS/@font-face/font-display))

_If an option is missing. Plz leave a feature request._

## Tip

You can load the entire Roboto font stack via a foreach loop.

```SCSS
$fonts-roboto: (
    'Light',
    'Light Italic',
    'Regular',
    'Italic',
    'Bold'
);

@each $variant in $fonts-roboto {
    @include font-face('Roboto', $variant);
}
```
