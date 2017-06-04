
* {string}

Gets and sets the password portion of the URL.

```js
const myURL = new URL('https://abc:xyz@example.com');
console.log(myURL.password);
  // Prints xyz

myURL.password = '123';
console.log(myURL.href);
  // Prints https://abc:123@example.com
```

Invalid URL characters included in the value assigned to the `password` property
are [percent-encoded][]. Note that the selection of which characters to
percent-encode may vary somewhat from what the [`url.parse()`][] and
[`url.format()`][] methods would produce.

