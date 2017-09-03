
* {string}

获取只读序列化的URL orgin部分。

```js
const { URL } = require('url');
const myURL = new URL('https://example.org/foo/bar?baz');
console.log(myURL.origin);
  // 输出 https://example.org
```

```js
const { URL } = require('url');
const idnURL = new URL('https://你好你好');
console.log(idnURL.origin);
  // 输出 https://xn--6qqa088eba

console.log(idnURL.hostname);
  // 输出 xn--6qqa088eba
```

