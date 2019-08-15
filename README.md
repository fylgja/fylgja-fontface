# Fylgja - FontFace

[![NPM version](https://img.shields.io/npm/v/@fylgja/fontface.svg)](https://www.npmjs.org/package/@fylgja/fontface)

The Fylgja font-face mixin makes it super easy to load fonts.

It will set all required settings for a good font-face automatically.
Which are still configurable if needed.

<details><summary>Table of Contents</summary>

- [Installation](#installation)
- [How to use](#how-to-use)
- [Config](#config)
- [Tips](#tips)
  - [Loop](#loop)
  - [Icons](#icons)
- [FAQ](#faq)

</details>

## Installation

```bash
npm i -D @fylgja/fontface
```

## How to use

Include the font-face package in to your code via;

```scss
// scss (DartSass) (LibSass >= 3.6.0)
@import "@fylgja/fontface";
// scss (older option)
@import "@fylgja/fontface/index";
```

To load a font.
Call the font-face mixin.
Add your font name + suffix of the font.

_All the other steps will be created by the mixin automatically,_
_(See [config](#config))._

**Input:**

```scss
@include font-face("Roboto", "Bold Italic");
```

**Output:**

```css
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

For this reason it is better to call a specific option.
Instead changing the complete mixin options.
Until you've reached the option you need to change.

**Examples;**

Bad way:

```scss
@include font-face("Roboto", "Regular", 400, "U+0-10FFFF", "../assets");
```

Good way:

```scss
@include font-face("Roboto", "Regular", $path: "../assets");
```

| Options      | Default value      | Description                         |
| ------------ | ------------------ | ----------------------------------- |
| `$name`      |                    | Name of the font family             |
| `$suffix`    | _null_             | Suffix (e.g. Regular or Bold)       |
| `$styles`    | $suffix            | Styles (e.g. 700i or 700 italic)    |
| `$unicode`   | $u-latin           | Unicode range of the the font face. |
| `$path`      | '../fonts'         | Path to the font file               |
| `$file-name` | _null_             | File name of the font               |
| `$formats`   | local, woff2, woff | The file formats of the font-face.  |
| `$load`      | swap               | Loading option of the font          |

_If an option is NULL it will be filled in by the font-face defaults_

_If an option is missing. Plz leave a feature request._

## Tips

### Loop

You can load the entire Roboto font stack via a foreach loop.

```scss
$fonts-roboto: (
    "Light",
    "Light Italic",
    "Regular",
    "Italic",
    "Bold"
);

@each $styles in $fonts-roboto {
    @include font-face("Roboto", $styles);
}
```

### Icons

You can use this mixin to also load font icon libraries.
Simply call the mixin as describe above.
But leave the suffix field to its default value of _null_.

```SCSS
@include font-face("FontAwesome", $unicode: "U+0-10FFFF");
```

Or use the suffix value of `'Regular'`

```scss
@include font-face("Material Icons", "Regular", $unicode: "U+0-10FFFF");
```

This will set by default the:
* font-weight to 400
* font-style to normal

You must still set the `$unicode`,
since icon libraries have a diffrent one than just Latin.
The default for the unicode is `U+0-10FFFF` which is all unicodes.

## FAQ

<details><summary>Why is the name different from the file</summary>

This is a little thing that came with the first publish.
Sadly this is stuck to the repo.

But I am not planing to change this
Since then I have to deprecate this one and republish a new font-face repo.

</details>

<details><summary>How do I use this with Variable Fonts</summary>

If you are planing to use variable fonts you don't need this.

This makes loading font-families easier
and is over kill for just one font-face.

</details>
