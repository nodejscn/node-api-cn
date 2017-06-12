
* {string}

Gets and sets the host portion of the URL.

```js
const { URL } = require('url');
const myURL = new URL('https://example.org:81/foo');
console.log(myURL.host);
  // Prints example.org:81

myURL.host = 'example.com:82';
console.log(myURL.href);
  // Prints https://example.com:82/foo
```

Invalid host values assigned to the `host` property are ignored.

