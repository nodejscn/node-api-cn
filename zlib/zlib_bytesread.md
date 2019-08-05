<!-- YAML
added: v8.1.0
deprecated: v10.0.0
-->

> Stability: 0 - Deprecated: Use [`zlib.bytesWritten`][] instead.

* {number}

Deprecated alias for [`zlib.bytesWritten`][]. This original name was chosen
because it also made sense to interpret the value as the number of bytes
read by the engine, but is inconsistent with other streams in Node.js that
expose values under these names.

