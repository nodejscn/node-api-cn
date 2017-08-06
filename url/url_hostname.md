
* {string}

获取及设置URL的主机名(hostname)部分。 `url.host`和`url.hostname`之间的区别是`url.hostname`*不* 包含端口。

```js
const { URL } = require('url');
const myURL = new URL('https://example.org:81/foo');
console.log(myURL.hostname);
  // 输出 example.org

myURL.hostname = 'example.com:82';
console.log(myURL.href);
  // 输出 https://example.com:81/foo
```

如果给`hostname`属性设置的值是无效值，那么该值将被忽略。

