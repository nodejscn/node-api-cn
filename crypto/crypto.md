
> 稳定的: 2 - 稳定的

`crypto`模块提供了加密功能包括OpenSSL的哈希，HMAC，密码，解密，签名和验证功能的一系列封装。

使用`require('crypto')`来访问这个模块。

```js
const crypto = require('crypto');

const secret = 'abcdefg';
const hash = crypto.createHmac('sha256', secret)
                   .update('I love cupcakes')
                   .digest('hex');
console.log(hash);
// Prints:
//   c0fa1bc00531bd78ef38c628449c5102aeabd49b5dc3a2a516ea6ea959d6658e
```

