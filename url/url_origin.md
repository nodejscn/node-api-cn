
* {string}

获取只读的序列化的 URL 的 origin。

```js
const myURL = new URL('https://example.org/foo/bar?baz');
console.log(myURL.origin);
  // 打印 https://example.org
```

```js
const idnURL = new URL('https://測試');
console.log(idnURL.origin);
// 打印 https://xn--g6w251d

console.log(idnURL.hostname);
// 打印 xn--g6w251d
```

