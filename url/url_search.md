
* {string}

Gets and sets the serialized query portion of the URL.

```js
const { URL } = require('url');
const myURL = new URL('https://example.org/abc?123');
console.log(myURL.search);
  // Prints ?123

myURL.search = 'abc=xyz';
console.log(myURL.href);
  // Prints https://example.org/abc?abc=xyz
```

Any invalid URL characters appearing in the value assigned the `search`
property will be [percent-encoded][]. Note that the selection of which
characters to percent-encode may vary somewhat from what the [`url.parse()`][]
and [`url.format()`][] methods would produce.

