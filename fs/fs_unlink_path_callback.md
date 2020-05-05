<!-- YAML
added: v0.0.2
changes:
  - version: v10.0.0
    pr-url: https://github.com/nodejs/node/pull/12562
    description: 参数 `callback` 不再是可选的。 
      如果不传入，则在运行时会抛出 `TypeError`。
  - version: v7.6.0
    pr-url: https://github.com/nodejs/node/pull/10739
    description: 参数 `path` 可以是 WHATWG `URL` 对象（使用 `file:` 协议）。 
      该支持目前仍是实验的。
  - version: v7.0.0
    pr-url: https://github.com/nodejs/node/pull/7897
    description: 参数 `callback` 不再是可选的。 
      如果不传入，则会触发弃用警告（id 为 DEP0013）。
-->

* `path` {string|Buffer|URL}
* `callback` {Function}
  * `err` {Error}

异步地删除文件或符号链接。
除了可能的异常，完成回调没有其他参数。

```js
// 假设 '文件.txt' 是普通的文件。
fs.unlink('文件.txt', (err) => {
  if (err) throw err;
  console.log('文件已被删除');
});
```

`fs.unlink()` 对空或非空的目录均不起作用。
若要删除目录，则使用 [`fs.rmdir()`]。

也可参见 unlink(2)。

