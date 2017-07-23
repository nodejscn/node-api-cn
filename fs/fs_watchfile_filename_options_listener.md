<!-- YAML
added: v0.1.31
changes:
  - version: v7.6.0
    pr-url: https://github.com/nodejs/node/pull/10739
    description: The `filename` parameter can be a WHATWG `URL` object using
                 `file:` protocol. Support is currently still *experimental*.
-->

* `filename` {string|Buffer|URL}
* `options` {Object}
  * `persistent` {boolean} **Default:** `true`
  * `interval` {integer} **Default:** `5007`
* `listener` {Function}

监视 `filename` 的变化。
回调 `listener` 会在每次访问文件时被调用。

`options` 参数可被省略。
如果提供的话，它应该是一个对象。
`options` 对象可能包含一个名为 `persistent` 的布尔值，表明当文件正在被监视时，进程是否应该继续运行。
`options` 对象可以指定一个 `interval` 属性，表示目标应该每隔多少毫秒被轮询。
默认值为 `{ persistent: true, interval: 5007 }`。

`listener` 有两个参数，当前的状态对象和以前的状态对象：

```js
fs.watchFile('message.text', (curr, prev) => {
  console.log(`the current mtime is: ${curr.mtime}`);
  console.log(`the previous mtime was: ${prev.mtime}`);
});
```

These stat objects are instances of `fs.Stat`.
这里的状态对象是 `fs.Stat` 实例。

如果你想在文件被修改而不只是访问时得到通知，则需要比较 `curr.mtime` 和 `prev.mtime`。

注意：当一个 `fs.watchFile` 的运行结果是一个 `ENOENT` 错误时，它会调用监听器一次，且将所有字段置零（或将日期设为 Unix 纪元）。
在 Windows 中，`blksize` 和 `blocks` 字段会是 `undefined` 而不是零。
如果文件是在那之后创建的，则监听器会被再次调用，且带上最新的状态对象。
这是在 v0.10 版之后在功能上的变化。

注意：[`fs.watch()`] 比 `fs.watchFile` 和 `fs.unwatchFile` 更高效。
可能的话，应该使用 `fs.watch` 而不是 `fs.watchFile` 和 `fs.unwatchFile`。

