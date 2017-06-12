
* {string}

Gets the read-only serialization of the URL's origin. Unicode characters that
may be contained within the hostname will be encoded as-is without [Punycode][]
encoding.

```js
const { URL } = require('url');
const myURL = new URL('https://example.org/foo/bar?baz');
console.log(myURL.origin);
  // Prints https://example.org
```

```js
const { URL } = require('url');
const idnURL = new URL('https://你好你好');
console.log(idnURL.origin);
  // Prints https://你好你好

console.log(idnURL.hostname);
  // Prints xn--6qqa088eba
```

