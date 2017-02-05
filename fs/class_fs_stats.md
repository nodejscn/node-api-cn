<!-- YAML
added: v0.1.21
-->

从 [`fs.stat()`]、[`fs.lstat()`] 和 [`fs.fstat()`] 及其同步版本返回的对象都是该类型。

 - `stats.isFile()`
 - `stats.isDirectory()`
 - `stats.isBlockDevice()`
 - `stats.isCharacterDevice()`
 - `stats.isSymbolicLink()` (仅对 [`fs.lstat()`] 有效)
 - `stats.isFIFO()`
 - `stats.isSocket()`

对于一个普通文件，[`util.inspect(stats)`] 会返回一个类似如下的字符串：

```js
{
  dev: 2114,
  ino: 48064969,
  mode: 33188,
  nlink: 1,
  uid: 85,
  gid: 100,
  rdev: 0,
  size: 527,
  blksize: 4096,
  blocks: 8,
  atime: Mon, 10 Oct 2011 23:24:11 GMT,
  mtime: Mon, 10 Oct 2011 23:24:11 GMT,
  ctime: Mon, 10 Oct 2011 23:24:11 GMT,
  birthtime: Mon, 10 Oct 2011 23:24:11 GMT
}
```

注意，`atime`、`mtime`、`birthtime` 和 `ctime` 是 [`Date`] 对象的实例，比较这些对象的值需要使用适当的方法。
对于大多数一般用途，[`getTime()`] 会返回 **1970年1月1日 00:00:00 UTC** 至今已过的毫秒数，且该整数应该满足任何对比，当然也有可用于显示模糊信息的其他方法。
详见 [MDN JavaScript 手册]。

