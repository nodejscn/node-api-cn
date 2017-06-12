
* {string}

Gets and sets the fragment portion of the URL.

```js
const { URL } = require('url');
const myURL = new URL('https://example.org/foo#bar');
console.log(myURL.hash);
  // Prints #bar

myURL.hash = 'baz';
console.log(myURL.href);
  // Prints https://example.org/foo#baz
```

Invalid URL characters included in the value assigned to the `hash` property
are [percent-encoded][]. Note that the selection of which characters to
percent-encode may vary somewhat from what the [`url.parse()`][] and
[`url.format()`][] methods would produce.

