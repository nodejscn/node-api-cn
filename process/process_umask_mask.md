<!-- YAML
added: v0.1.19
-->

* `mask` {string|integer}

`process.umask(mask)` 会设置 Node.js 进程的文件模式的创建掩码。 
子进程从父进程继承掩码。 
返回上一个掩码。

```js
const newmask = 0o022;
const oldmask = process.umask(newmask);
console.log(
  `将 umask 从 ${oldmask.toString(8)} 更改为 ${newmask.toString(8)}`
);
```

在 [`Worker`] 线程中，`process.umask(mask)` 会抛出异常。


