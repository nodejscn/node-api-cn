<!-- YAML
added: v10.5.0
changes:
  - version: v12.8.0
    pr-url: https://github.com/nodejs/node/pull/28799
    description: The `maxmem` value can now be any safe integer.
  - version: v10.9.0
    pr-url: https://github.com/nodejs/node/pull/21525
    description: The `cost`, `blockSize` and `parallelization` option names
                 have been added.
-->

* `password` {string|Buffer|TypedArray|DataView}
* `salt` {string|Buffer|TypedArray|DataView}
* `keylen` {number}
* `options` {Object}
  * `cost` {number} CPU 或内存的成本参数。必须是 2 的次方且大于1。**默认值:** `16384`。
  * `blockSize` {number} 块大小参数。**默认值:** `8`。
  * `parallelization` {number} 并行化参数。**默认值:** `1`。
  * `N` {number} `cost` 的别名。只能指定两者之一。
  * `r` {number} `blockSize` 的别名。只能指定两者之一。
  * `p` {number} `parallelization` 的别名。只能指定两者之一。
  * `maxmem` {number} 内存的上限。当（大约） `128 * N * r > maxmem` 时是错误的。**默认值:** `32 * 1024 * 1024`。
* `callback` {Function}
  * `err` {Error}
  * `derivedKey` {Buffer}


提供异步的 [scrypt] 实现。 
Scrypt 是一个基于密码的密钥派生函数，被设计为在计算和内存方面都非常高成本，目的是使暴力破解无法成功。

`salt` 应尽可能独特。 
建议盐值是随机的并且至少 16 个字节长。 
有关详细信息，请参阅 [NIST SP 800-132]。

`callback` 函数有两个参数：`err` 和 `derivedKey`。 
当密钥派生失败时，`err` 是一个异常对象，否则 `err` 为 `null`。 
`derivedKey` 会作为 [`Buffer`] 传给回调。

当任何的输入参数指定了无效的值或类型时，会抛出异常。

```js
const crypto = require('crypto');
// 使用出厂默认值。
crypto.scrypt('密码', '盐值', 64, (err, derivedKey) => {
  if (err) throw err;
  console.log(derivedKey.toString('hex'));  // '00d9e09...8a4f15a'
});
// 使用自定义的 N 参数。必须是 2 的次方。
crypto.scrypt('密码', '盐值', 64, { N: 1024 }, (err, derivedKey) => {
  if (err) throw err;
  console.log(derivedKey.toString('hex'));  // 'f710b45...f04e377'
});
```

