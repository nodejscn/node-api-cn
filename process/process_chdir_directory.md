<!-- YAML
added: v0.1.17
-->

* `directory` {string}

`process.chdir()` 方法变更 Node.js 进程的当前工作目录，如果变更目录失败会抛出异常（例如，如果指定的 `directory` 不存在）。

```js
console.log(`Starting directory: ${process.cwd()}`);
try {
  process.chdir('/tmp');
  console.log(`New directory: ${process.cwd()}`);
} catch (err) {
  console.error(`chdir: ${err}`);
}
```

此特性在 [`Worker`] 线程中不可用。

