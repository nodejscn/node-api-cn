
* {string}

Gets and sets the username portion of the URL.

```js
const { URL } = require('url');
const myURL = new URL('https://abc:xyz@example.com');
console.log(myURL.username);
  // Prints abc

myURL.username = '123';
console.log(myURL.href);
  // Prints https://123:xyz@example.com/
```

Any invalid URL characters appearing in the value assigned the `username`
property will be [percent-encoded][]. Note that the selection of which
characters to percent-encode may vary somewhat from what the [`url.parse()`][]
and [`url.format()`][] methods would produce.

