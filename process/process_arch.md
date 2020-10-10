<!-- YAML
added: v0.5.0
-->

* {string}

为其编译 Node.js 二进制文件的操作系统的 CPU 架构。
可能的值有：`'arm'`、`'arm64'`、`'ia32'`、`'mips'`、`'mipsel'`、`'ppc'`、`'ppc64'`、`'s390'`、`'s390x'`、`'x32'` 和 `'x64'`。

```js
console.log(`该处理器的架构是 ${process.arch}`);
```

