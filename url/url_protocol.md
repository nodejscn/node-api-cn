
* {string}

Gets and sets the protocol portion of the URL.

```js
const { URL } = require('url');
const myURL = new URL('https://example.org');
console.log(myURL.protocol);
  // Prints https:

myURL.protocol = 'ftp';
console.log(myURL.href);
  // Prints ftp://example.org/
```

Invalid URL protocol values assigned to the `protocol` property are ignored.

