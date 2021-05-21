
It is possible to construct a WHATWG URL from component parts using either the
property setters or a template literal string:

```js
const myURL = new URL('https://example.org');
myURL.pathname = '/a/b/c';
myURL.search = '?d=e';
myURL.hash = '#fgh';
```

```js
const pathname = '/a/b/c';
const search = '?d=e';
const hash = '#fgh';
const myURL = new URL(`https://example.org${pathname}${search}${hash}`);
```

To get the constructed URL string, use the `href` property accessor:

```js
console.log(myURL.href);
```

