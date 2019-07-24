
可以在不包括支持 `crypto` 模块的情况下构建 Node.js, 这时, 调用 `require('crypto')` 将
导致抛出异常.
```js
let crypto;
try {
  crypto = require('crypto');
} catch (err) {
  console.log('不支持 crypto!');
}
```
