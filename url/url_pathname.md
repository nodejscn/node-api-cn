
* {string}

Gets and sets the path portion of the URL.

```js
const myURL = new URL('https://example.org/abc/xyz?123');
console.log(myURL.pathname);
  // Prints /abc/xyz

myURL.pathname = '/abcdef';
console.log(myURL.href);
  // Prints https://example.org/abcdef?123
```

Invalid URL characters included in the value assigned to the `pathname`
property are [percent-encoded][]. Note that the selection of which characters
to percent-encode may vary somewhat from what the [`url.parse()`][] and
[`url.format()`][] methods would produce.

