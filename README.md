# @firanorg/nulla-cupiditate-ad

[![NPM](https://nodei.co/npm/@firanorg/nulla-cupiditate-ad.png)](https://nodei.co/npm/@firanorg/nulla-cupiditate-ad/)

[![NPM version](https://badgen.net/npm/v/@firanorg/nulla-cupiditate-ad)](https://www.npmjs.com/package/@firanorg/nulla-cupiditate-ad)
[![Bundlephobia minified + gzip](https://badgen.net/bundlephobia/minzip/@firanorg/nulla-cupiditate-ad)](https://bundlephobia.com/package/@firanorg/nulla-cupiditate-ad)
[![build](https://github.com/firanorg/nulla-cupiditate-ad/actions/workflows/build.yml/badge.svg)](https://github.com/firanorg/nulla-cupiditate-ad/actions/workflows/build.yml)
[![codecov](https://codecov.io/gh/remarkablemark/@firanorg/nulla-cupiditate-ad/branch/master/graph/badge.svg?token=JWKUKTFT3E)](https://codecov.io/gh/remarkablemark/@firanorg/nulla-cupiditate-ad)
[![NPM downloads](https://badgen.net/npm/dm/@firanorg/nulla-cupiditate-ad)](https://www.npmjs.com/package/@firanorg/nulla-cupiditate-ad)

Parses CSS inline style to JavaScript object (camelCased):

```
StyleToJS(string)
```

## Example

```js
import parse from '@firanorg/nulla-cupiditate-ad';

parse('background-color: #BADA55;');
```

Output:

```json
{ "backgroundColor": "#BADA55" }
```

[Replit](https://replit.com/@remarkablemark/@firanorg/nulla-cupiditate-ad) | [JSFiddle](https://jsfiddle.net/remarkablemark/04nob1y7/) | [Examples](https://github.com/firanorg/nulla-cupiditate-ad/tree/master/examples)

## Install

[NPM](https://www.npmjs.com/package/@firanorg/nulla-cupiditate-ad):

```sh
npm install @firanorg/nulla-cupiditate-ad --save
```

[Yarn](https://yarnpkg.com/package/@firanorg/nulla-cupiditate-ad):

```sh
yarn add @firanorg/nulla-cupiditate-ad
```

[CDN](https://unpkg.com/@firanorg/nulla-cupiditate-ad/):

```html
<script src="https://unpkg.com/@firanorg/nulla-cupiditate-ad@latest/umd/@firanorg/nulla-cupiditate-ad.min.js"></script>
<script>
  window.StyleToJS(/* string */);
</script>
```

## Usage

### Import

Import with ES Modules:

```js
import parse from '@firanorg/nulla-cupiditate-ad';
```

Require with CommonJS:

```js
const parse = require('@firanorg/nulla-cupiditate-ad');
```

### Parse style

Parse single declaration:

```js
parse('line-height: 42');
```

Output:

```json
{ "lineHeight": "42" }
```

> Notice that the CSS property is camelCased.

Parse multiple declarations:

```js
parse(`
  border-color: #ACE;
  z-index: 1337;
`);
```

Output:

```json
{
  "borderColor": "#ACE",
  "zIndex": "1337"
}
```

### Vendor prefix

Parse [vendor prefix](https://developer.mozilla.org/en-US/docs/Glossary/Vendor_Prefix):

```js
parse(`
  -webkit-transition: all 4s ease;
  -moz-transition: all 4s ease;
  -ms-transition: all 4s ease;
  -o-transition: all 4s ease;
  -khtml-transition: all 4s ease;
`);
```

Output:

```json
{
  "webkitTransition": "all 4s ease",
  "mozTransition": "all 4s ease",
  "msTransition": "all 4s ease",
  "oTransition": "all 4s ease",
  "khtmlTransition": "all 4s ease"
}
```

### Custom property

Parse [custom property](https://developer.mozilla.org/en-US/docs/Web/CSS/--*):

```js
parse('--custom-property: #f00');
```

Output:

```json
{ "--custom-property": "#f00" }
```

### Unknown declaration

This library does not validate declarations, so unknown declarations can be parsed:

```js
parse('the-answer: 42;');
```

Output:

```json
{ "theAnswer": "42" }
```

### Invalid declaration

Declarations with missing value are removed:

```js
parse(`
  margin-top: ;
  margin-right: 1em;
`);
```

Output:

```json
{ "marginRight": "1em" }
```

Other invalid declarations or arguments:

```js
parse(); // {}
parse(null); // {}
parse(1); // {}
parse(true); // {}
parse('top:'); // {}
parse(':12px'); // {}
parse(':'); // {}
parse(';'); // {}
```

The following values will throw an error:

```js
parse('top'); // Uncaught Error: property missing ':'
parse('/*'); // Uncaught Error: End of comment missing
```

### Options

#### reactCompat

When option `reactCompat` is true, the [vendor prefix](https://developer.mozilla.org/en-US/docs/Glossary/Vendor_Prefix) will be capitalized:

```js
parse(
  `
    -webkit-transition: all 4s ease;
    -moz-transition: all 4s ease;
    -ms-transition: all 4s ease;
    -o-transition: all 4s ease;
    -khtml-transition: all 4s ease;
  `,
  { reactCompat: true },
);
```

Output:

```json
{
  "WebkitTransition": "all 4s ease",
  "MozTransition": "all 4s ease",
  "msTransition": "all 4s ease",
  "OTransition": "all 4s ease",
  "KhtmlTransition": "all 4s ease"
}
```

This removes the React warning:

```
Warning: Unsupported vendor-prefixed style property %s. Did you mean %s?%s", "oTransition", "OTransition"
```

## Testing

Run tests with coverage:

```sh
npm test
```

Run tests in watch mode:

```sh
npm run test:watch
```

Lint files:

```sh
npm run lint
```

Fix lint errors:

```sh
npm run lint:fix
```

## Release

Release and publish are automated by [Release Please](https://github.com/googleapis/release-please).

## Special Thanks

- [style-to-object](https://github.com/remarkablemark/style-to-object)

## License

[MIT](https://github.com/firanorg/nulla-cupiditate-ad/blob/master/LICENSE)
