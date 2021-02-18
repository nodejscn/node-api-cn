<!-- YAML
added: v0.1.17
-->

* `directory` {string}

`process.chdir()` 方法可以变更 Node.js 进程的当前工作目录，如果操作失败（例如，指定的 `directory` 不存在）则抛出异常。

```js
console.log(`起始的目录: ${process.cwd()}`);
try {
  process.chdir('/tmp');
  console.log(`新的目录: ${process.cwd()}`);
} catch (err) {
  console.error(`chdir: ${err}`);
}
```

此特性在 [`Worker`] 线程中不可用。

