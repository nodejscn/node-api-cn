<!-- YAML
added: v0.1.21
changes:
  - version: v8.1.0
    pr-url: https://github.com/nodejs/node/pull/13173
    description: Added times as numbers.
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

```console
Stats {
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
  atimeMs: 1318289051000.1,
  mtimeMs: 1318289051000.1,
  ctimeMs: 1318289051000.1,
  birthtimeMs: 1318289051000.1,
  atime: Mon, 10 Oct 2011 23:24:11 GMT,
  mtime: Mon, 10 Oct 2011 23:24:11 GMT,
  ctime: Mon, 10 Oct 2011 23:24:11 GMT,
  birthtime: Mon, 10 Oct 2011 23:24:11 GMT }
```

*注意*: `atimeMs`, `mtimeMs`, `ctimeMs`, `birthtimeMs` 是以单位为毫秒保存相对应时间的数字 [numbers][MDN-Number].
他们的精度由所在的平台决定. `atime`, `mtime`, `ctime` 以及 `birthtime` 是表示各个时间的日期对象 `[Date][MDN-Date]`.
`Date` 与 数值并没有关联. 对数值进行重新赋值, 或者改变 `Date` 的值, 不会反映到相对应的表示中.




