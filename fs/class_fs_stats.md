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

*Note*: `atimeMs`, `mtimeMs`, `ctimeMs`, `birthtimeMs` are [numbers][MDN-Number]
that hold the corresponding times in milliseconds. Their precision is platform
specific. `atime`, `mtime`, `ctime`, and `birthtime` are [`Date`][MDN-Date]
object alternate representations of the various times. The `Date` and number
values are not connected. Assigning a new number value, or mutating the `Date`
value, will not be reflected in the corresponding alternate representation.

