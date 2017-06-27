<!-- YAML
added: v0.1.16
-->

* {string}

`process.platform`属性返回字符串，标识Node.js进程运行其上的操作系统平台。
例如`'darwin'`, `'freebsd'`, `'linux'`, `'sunos'` 或 `'win32'`

```js
console.log(`This platform is ${process.platform}`);
```

