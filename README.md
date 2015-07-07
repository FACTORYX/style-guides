# FactoryX CSS (Stylus) Style guide

## Mixin libraries used:
- nib
- jeet

## Default elements
Broadly, default html elements are to be avoided.

**Avoid:**
`h1, h2...
nav, header, footer, b`

Instead add styles to div elements. This makes it more modular and customizable without prior browser-specific styles added.

```coffee
div className: 'header'
```

```stylus
.header
  font-size: 2.5em
  margin: 2em 25%
```

Exceptions:
`p` (paragraphs) are allowed as they do not carry style.


## Globals
Globals are to be avoided unless it is a site-wide reset:

**Allowed:**
```stylus
*, *:before, *:after
  box-sizing: border-box
```

**Wrong:**

```stylus
div
  padding: 10px
  color: green
```

## Property order
```
[selector]
  mixins
  position
  size
  padding
  margin
  background/colors
  borders/shadows/outlines
  font/text
  transforms/animations
  transitions
  z-index

```

## Mixins
Mixins are defined as follows:
- camelCase
- extend-able
- should have defaults

```stylus
button(color=#555)
  padding: 10px
  background: color

largeButton(color=#555)
  button(color)
  padding: 25px
  // ...
```

## Pseudo selectors
When adding a pseudo class to a selector use the `&` prefix.
```stylus
.element
  background: #000
  &.blue
    background: #0000ff
```

The same applies to pseudo classes + states, unless a single line.

```stylus
.element
  color: #000
  &:hover
    color: #171717

// This is fine as it does not have any other state style:
.other:before
  color: #171717

```


## Property rules

- use clockwise order when a property has more than one polygonal argument
- never use 0px, default to 0
- decimal measurements do not have a preceding 0, use .2s instead of 0.2s
- pixels do not have percentages. Use whole numbers.

#### Background
Use `background` not `background-color` for both images and colors.

**Wrong:**
```stylus
.element
  background: url('/img/bg.png')
  background-color: #555
```

**Right:**
```stylus
.element
  background: #555 url('/img/bg.png')
```

Exception: When there is a need to have the background color change but keep the image:
```stylus
.element
  background: #000 url('/img/bg.png')
  &.grey
    background-color: #555
```

#### Position
```stylus
.element
  absolute: top 25% right 5vw left 5vw
```


#### Margin / Padding

Combine properties if more than one property is used.

**Wrong:**
```stylus
.element
  margin-top: 20px
  margin-bottom: 20px
  padding-left: 25%
  padding-top: 50px
```

**Right:**
```stylus
.element
  margin: 20px 0
  padding: 50px 0 0 25%
```

## Selector names

Selector names (className in react.js) are to be defined as follows:

- hyphened, not camelcase `login-component`, not `loginComponent`. Never use underscores
- short and descriptive. `profile-view`, not `user-profile-view`
- sub-selectors are to be short: `profile-view` > `name`

```stylus
.profile-view
  align(direction=horizontal)
  background: #fff
  .name
    font-size: largeFont
  .email
    font-weight: bold

```
