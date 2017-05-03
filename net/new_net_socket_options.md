<!-- YAML
added: v0.3.4
-->

构造一个新的socket对象。

`options` 是一个对象，有着以下默认值:

```js
{
  fd: null,
  allowHalfOpen: false,
  readable: false,
  writable: false
}
```

`fd` 允许你指定socket的存在的文件描述器。
设定 `readable` 和/或 `writable` 为 `true` 来允许在这个socket上进行读和/或写。
(注意: 只有当 `fd` 被传参时，才工作).
关于 `allowHalfOpen`, 请参照 [`net.createServer()`] 和 [`'end'`] 事件.

`net.Socket` 是 [`EventEmitter`][] 实例，有以下事件:

