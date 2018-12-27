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
  * `persistent` {boolean} 默认为 `true`。
  * `interval` {integer} 默认为 `5007`。
* `listener` {Function}
  * `current` {fs.Stats}
  * `previous` {fs.Stats}

监视 `filename` 的变化。
每当文件被访问时会调用 `listener`。

`options` 对象可以有一个布尔值的 `persistent` 属性，表明当文件正在被监视时，进程是否继续运行。
`options` 对象可以指定一个 `interval` 属性，指定目标每隔多少毫秒被轮询。
默认值为 `{ persistent: true, interval: 5007 }`。

`listener` 有两个参数，当前的状态对象和以前的状态对象：

```js
fs.watchFile('文件.text', (curr, prev) => {
  console.log(`当前的最近修改时间是: ${curr.mtime}`);
  console.log(`之前的最近修改时间是: ${prev.mtime}`);
});
```

这里的状态对象是 `fs.Stat` 实例。

如果想在文件被修改而不只是访问时得到通知，则需要比较 `curr.mtime` 和 `prev.mtime`。

当 `fs.watchFile` 的运行结果是一个 `ENOENT` 错误时，它会调用监听器一次，且将所有字段置零（或将日期设为 Unix 纪元）。
在 Windows 中，`blksize` 和 `blocks` 字段会是 `undefined` 而不是零。
如果文件是在那之后创建的，则监听器会被再次调用，且带上最新的状态对象。
这是在 v0.10 版之后在功能上的变化。

[`fs.watch()`] 比 `fs.watchFile` 和 `fs.unwatchFile` 更高效。
建议使用 `fs.watch` 而不是 `fs.watchFile` 和 `fs.unwatchFile`。

当 `fs.watchFile()` 所监听的文件消失并重新出现时，回调事件第二次返回的 `previousStat`（文件重新出现）会与第一次返回的 `previousStat`（文件消失）相同。

这种情况会发生在:
- 文件被删除，然后又恢复。
- 文件被重命名两次，且第二次重命名与其原名称相同。

