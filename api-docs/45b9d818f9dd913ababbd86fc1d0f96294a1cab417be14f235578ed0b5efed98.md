<!-- YAML
added: v0.2.0
changes:
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

<!-- eslint-skip -->
```js
{ http_parser: '2.7.0',
  node: '8.9.0',
  v8: '6.3.292.48-node.6',
  uv: '1.18.0',
  zlib: '1.2.11',
  ares: '1.13.0',
  modules: '60',
  nghttp2: '1.29.0',
  napi: '2',
  openssl: '1.0.2n',
  icu: '60.1',
  unicode: '10.0',
  cldr: '32.0',
  tz: '2016b' }
```
