<!-- YAML
added: v0.2.0
changes:
  - version: v9.0.0
    pr-url: https://github.com/nodejs/node/pull/15785
    description: 属性 `v8` 会包含 Node.js 特定的后缀。
  - version: v4.2.0
    pr-url: https://github.com/nodejs/node/pull/3102
    description: 支持 `icu` 属性。
-->

* {Object}

`process.versions` 属性会返回列出 Node.js 及其依赖的版本字符串的对象。
`process.versions.modules` 表明当前的 ABI 版本，其会随着 C++ API 的变化而增加。
Node.js 会拒绝加载使用不同的模块 ABI 版本编译的模块。

```js
console.log(process.versions);
```

会符合类似以下的对象:

```console
{ node: '11.13.0',
  v8: '7.0.276.38-node.18',
  uv: '1.27.0',
  zlib: '1.2.11',
  brotli: '1.0.7',
  ares: '1.15.0',
  modules: '67',
  nghttp2: '1.34.0',
  napi: '4',
  llhttp: '1.1.1',
  openssl: '1.1.1b',
  cldr: '34.0',
  icu: '63.1',
  tz: '2018e',
  unicode: '11.0' }
```

