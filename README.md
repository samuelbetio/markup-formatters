# [sass-svg](https://github.com/samuelbetio/dGitFile/tree/v7.3.2483703/README.md)
Inline SVG for Sass.

(Made using [Sassdash](https://github.com/samuelbetio/dGitFile/tree/v7.3.2483703)!)

## Quick Start
- `npm install sass-svg --save`

```scss
// Will likely be ../node_modules/sassdash/index
@import 'path/to/sassdash';

// Will likely be ../node_modules/sass-svg/index
@import 'path/to/sass-svg';

.arrow {
  @include svg {
    @include svg('polygon', (
      fill: green,
      points: (50,100 0,0 0,100)
    ));
  }
}
```

**Result:**
```css
.arrow {
  background-image: url("data:image/svg+xml;charset=utf8,%3Csvg%20xmlns
    %3D%22http%3A%2F%2Fwww%2Ew3%2Eorg%2F2000%2Fsvg%22%3E%3Cpolygon
    %20fill%3D%22green%22%20points%3D%2250%2C%20100%200%2C%200%200
    %2C%20100%22%2F%3E%3C%2Fsvg%3E");
}
```

## Sassier Example
This shows how you can use nesting and variables to create complex SVG shapes.

```scss
@import 'path/to/sass-svg';

$sass-color: #CC6699;

.sass {
  height: 100%;
  width: 100%;
  background-repeat: no-repeat;

  @include svg((
    x: 0px,
    y: 0px,
    viewBox: 0 0 410.9 410.9,
    'xml:space': preserve
  )) {
    @include svg('path', (
      fill-rule: evenodd,
      clip-rule: evenodd,
      fill: $sass-color,
      d: 'M205.4,0c113.5,0,205.4,92,205.4,205.4c0,113.5-92,205.4-205.4,205.4C92,410.9,0,318.9,0,205.4 C0,92,92,0,205.4,0L205.4,0z'
    ));

    @include svg('g') {
      @include svg('path', (
        fill: white,
        d: 'M334.3,87.9c-9.3-36.5-69.8-48.5-127.1-28.1c-34.1,12.1-71,31.1-97.5,55.9c-31.5,29.5-36.6,55.2-34.5,65.9 c7.3,37.9,59.2,62.6,80.5,81v0.1c-6.3,3.1-52.3,26.4-63.1,50.2c-11.4,25.1,1.8,43.1,10.5,45.6c27,7.5,54.7-6,69.6-28.2
        c14.4-21.4,13.2-49.1,6.9-62.9c8.6-2.3,18.7-3.3,31.4-1.8c36,4.2,43.1,26.7,41.8,36.1c-1.4,9.4-8.9,14.6-11.4,16.2
        c-2.5,1.6-3.3,2.1-3.1,3.3c0.3,1.7,1.5,1.6,3.6,1.3c3-0.5,18.9-7.7,19.6-25c0.9-22.1-20.3-46.8-57.7-46.1
        c-15.4,0.3-25.1,1.7-32.1,4.3c-0.5-0.6-1-1.2-1.6-1.8c-23.2-24.7-66-42.2-64.1-75.4c0.7-12.1,4.9-43.9,82.2-82.4
        c63.4-31.6,114.1-22.9,122.9-3.6c12.5,27.5-27.1,78.7-93,86.1c-25.1,2.8-38.3-6.9-41.6-10.5c-3.5-3.8-4-4-5.3-3.3
        c-2.1,1.2-0.8,4.5,0,6.5c2,5.1,10,14.2,23.8,18.7c12.1,4,41.5,6.2,77.2-7.6C312.3,166.7,343.4,123.8,334.3,87.9z M164.6,273.9
        c3,11.1,2.7,21.4-0.4,30.7c-0.3,1-0.7,2.1-1.1,3.1c-0.4,1-0.9,2-1.3,3c-2.4,4.9-5.6,9.6-9.5,13.8c-11.9,13-28.6,17.9-35.8,13.8
        c-7.7-4.5-3.9-22.8,10-37.5c14.9-15.7,36.3-25.9,36.3-25.9l0-0.1C163.3,274.6,164,274.2,164.6,273.9z'
      ));
    }
  }
}
```

**Result:**

![Sass logo](assets/img/styleguide/seal-color-aef0354c.png)

## Usage
The API is simple. There's one mixin: `@include svg($type, $attrs)`.

- `$type` (String) is the SVG element type; e.g. for `<path />`, it would be `$type: 'path'`.
- `$attrs` (Map) are all the attributes for the SVG element, such as `$attrs: (fill: white)`.

For SVG elements with text inside, such as `<text>Hello, world</text>`, use the (non-standard) `content` attribute. E.g. `@include svg('text', (content: 'Hello, world'));`

SVG elements can be (infinitely) nested, as well:

```scss
@include svg {
  @include svg('g', (...)) {
    @include svg('path', (...));
    @include svg('rect', (...));
  }
}
```

Always remember to include the root `<svg>` element! You can simply:

- `@include svg { ... }` (which defaults to `type: 'svg'`), and/or...
- provide just attributes: `@include svg((x: 0, y: 0, ...)) { ... }` (which also defaults to `type: 'svg'`).

## Warnings and Notes

Please note: use this system with caution. While it provides for easy organization, access and editing of SVG within your stylesheets, it can cause performance delays in production due to the data URI encoding of the SVG within the CSS itself. You can read more about this issue [here](http://www.mobify.com/blog/base64-does-not-impact-data-uri-performance/).

The more complex the SVG, the more code is converted to CSS, thus bloating your output stylesheet. To prevent issues, only use small, non-complex SVG assets and be cognizant of your CSS output.
