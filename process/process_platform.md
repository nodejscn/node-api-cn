<!-- YAML
added: v0.1.16
-->

* {string}

`process.platform` 属性会返回标识操作系统平台（Node.js 进程运行其上的）的字符串。

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

如果 Node.js 构建于 Android 操作系统上，则也可能返回值为 `'android'`。 
但是，Node.js 中的 Android 支持是[实验性的][Android building]。


