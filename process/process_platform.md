<!-- YAML
added: v0.1.16
-->

* {string}

`process.platform`属性返回字符串，标识Node.js进程运行其上的操作系统平台。

例如

* `'aix'`
* `'darwin'`
* `'freebsd'`
* `'linux'`
* `'openbsd'`
* `'sunos'`
* `'win32'`

```js
console.log(`This platform is ${process.platform}`);
```

The value `'android'` may also be returned if the Node.js is built on the
Android operating system. However, Android support in Node.js
[is experimental][Supported platforms].

