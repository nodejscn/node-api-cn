
* {string}

Gets and sets the port portion of the URL.

```js
const { URL } = require('url');
const myURL = new URL('https://example.org:8888');
console.log(myURL.port);
  // Prints 8888

// Default ports are automatically transformed to the empty string
// (HTTPS protocol's default port is 443)
myURL.port = '443';
console.log(myURL.port);
  // Prints the empty string
console.log(myURL.href);
  // Prints https://example.org/

myURL.port = 1234;
console.log(myURL.port);
  // Prints 1234
console.log(myURL.href);
  // Prints https://example.org:1234/

// Completely invalid port strings are ignored
myURL.port = 'abcd';
console.log(myURL.port);
  // Prints 1234

// Leading numbers are treated as a port number
myURL.port = '5678abcd';
console.log(myURL.port);
  // Prints 5678

// Non-integers are truncated
myURL.port = 1234.5678;
console.log(myURL.port);
  // Prints 1234

// Out-of-range numbers are ignored
myURL.port = 1e10;
console.log(myURL.port);
  // Prints 1234
```

The port value may be set as either a number or as a String containing a number
in the range `0` to `65535` (inclusive). Setting the value to the default port
of the `URL` objects given `protocol` will result in the `port` value becoming
the empty string (`''`).

If an invalid string is assigned to the `port` property, but it begins with a
number, the leading number is assigned to `port`. Otherwise, or if the number
lies outside the range denoted above, it is ignored.

