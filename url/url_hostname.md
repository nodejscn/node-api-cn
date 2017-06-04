
* {string}

Gets and sets the hostname portion of the URL. The key difference between
`url.host` and `url.hostname` is that `url.hostname` does *not* include the
port.

```js
const myURL = new URL('https://example.org:81/foo');
console.log(myURL.hostname);
  // Prints example.org

myURL.hostname = 'example.com:82';
console.log(myURL.href);
  // Prints https://example.com:81/foo
```

Invalid hostname values assigned to the `hostname` property are ignored.

