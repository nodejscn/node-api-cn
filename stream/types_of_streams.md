
Node.js 中有四种基本的流类型：

* [Readable][] - 可读的流 (例如
  [`fs.createReadStream()`][]).
* [Writable][] - 可写的流 (例如
  [`fs.createWriteStream()`][]).
* [Duplex][] - 可读写的流 (例如
  [`net.Socket`][]).
* [Transform][] - 在读写过程中可以修改和变换数据的 Duplex 流  (例如 [`zlib.createDeflate()`][]).

