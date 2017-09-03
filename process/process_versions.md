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
{
  http_parser: '2.3.0',
  node: '1.1.1',
  v8: '4.1.0.14',
  uv: '1.3.0',
  zlib: '1.2.8',
  ares: '1.10.0-DEV',
  modules: '43',
  icu: '55.1',
  openssl: '1.0.1k',
  unicode: '8.0',
  cldr: '29.0',
  tz: '2016b' }
```

