
* Returns: {string}

The `toJSON()` method on the `URL` object returns the serialized URL. The
value returned is equivalent to that of [`url.href`][] and
[`url.toString()`][].

This method is automatically called when an `URL` object is serialized
with [`JSON.stringify()`][].

```js
const myURLs = [
  new URL('https://www.example.com'),
  new URL('https://test.example.org')
];
console.log(JSON.stringify(myURLs));
  // Prints ["https://www.example.com/","https://test.example.org/"]
```

