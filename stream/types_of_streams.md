
Node.js 中有四种基本的流类型：

* [`Writable`] - 可写入数据的流（例如 [`fs.createWriteStream()`]）。
* [`Readable`] - 可读取数据的流（例如 [`fs.createReadStream()`]）。
* [`Duplex`] - 可读又可写的流（例如 [`net.Socket`]）。
* [`Transform`] - 在读写过程中可以修改或转换数据的 `Duplex` 流（例如 [`zlib.createDeflate()`]）。

此外，该模块还包括实用函数 [`stream.pipeline()`]、[`stream.finished()`] 和 [`stream.Readable.from()`]。


