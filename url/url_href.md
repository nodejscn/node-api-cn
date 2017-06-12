
* {string}

Gets and sets the serialized URL.

```js
const { URL } = require('url');
const myURL = new URL('https://example.org/foo');
console.log(myURL.href);
  // Prints https://example.org/foo

myURL.href = 'https://example.com/bar';
console.log(myURL.href);
  // Prints https://example.com/bar
```

Getting the value of the `href` property is equivalent to calling
[`url.toString()`][].

Setting the value of this property to a new value is equivalent to creating a
new `URL` object using [`new URL(value)`][`new URL()`]. Each of the `URL`
object's properties will be modified.

If the value assigned to the `href` property is not a valid URL, a `TypeError`
will be thrown.

