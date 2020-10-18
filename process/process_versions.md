<!-- YAML
added: v0.2.0
changes:
  - version: v9.0.0
    pr-url: https://github.com/nodejs/node/pull/15785
    description: The `v8` property now includes a Node.js specific suffix.
  - version: v4.2.0
    pr-url: https://github.com/nodejs/node/pull/3102
    description: The `icu` property is now supported.
-->

* {Object}

`process.versions`属性返回一个对象，此对象列出了Node.js和其依赖的版本信息。
`process.versions.modules`表明了当前ABI版本，此版本会随着一个C++API变化而增加。
Node.js会拒绝加载模块，如果这些模块使用一个不同ABI版本的模块进行编译。

```js
console.log(process.versions);
```

会显示类似下面的对象信息:

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

