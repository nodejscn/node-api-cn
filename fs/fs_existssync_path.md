<!-- YAML
added: v0.1.21
changes:
  - version: v7.6.0
    pr-url: https://github.com/nodejs/node/pull/10739
    description: 参数 `path` 可以是 WHATWG `URL` 对象（使用 `file:` 协议）。 
      该支持目前仍是实验的。
-->

* `path` {string|Buffer|URL}
* 返回: {boolean}

如果路径存在，则返回 `true`，否则返回 `false`。

详见此 API 的异步版本的文档：[`fs.exists()`]。

虽然 `fs.exists()` 是弃用的，但 `fs.existsSync()` 不是弃用的。
`fs.exists()` 的 `callback` 参数接受的参数与其他的 Node.js 回调的不一致。
`fs.existsSync()` 不使用回调。

```js
if (fs.existsSync('文件')) {
  console.log('该路径已存在');
}
```

