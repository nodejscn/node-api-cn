<!-- YAML
added: v0.1.16
-->

* {string}

`process.platform` 属性返回字符串，标识 Node.js 进程运行其上的操作系统平台。

当前可能的值有：

* `'aix'`
* `'darwin'`
* `'freebsd'`
* `'linux'`
* `'openbsd'`
* `'sunos'`
* `'win32'`

```js
console.log(`此平台是 ${process.platform}`);
```

如果 Node.js 是在 Android 操作系统上构建的，也可以返回值 `'android'`。 
但是，Node.js 中的 Android 支持是[实验性的][Android building]。


