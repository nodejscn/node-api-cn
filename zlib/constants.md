<!-- YAML
added: v0.5.8
-->

<!--type=misc-->

这些被定义在 `zlib.h` 的全部常量同时也被定义在 `require('zlib').constants` 常量上.
不需要在正常的操作中使用这些常量. 记录他们为了使他们的存在并不奇怪. 这个章节几乎直接取自[zlib documentation].
参阅 <http://zlib.net/mamual.html#Constants> 获取更多信息.

*注意*: 以前, 可以直接从 `require('zlib')` 中获取到这些常量, 例如 `zlib.Z_NO_FLUSH`. 
目前仍然可以从模块中直接访问这些常量, 但是不推荐使用.

可接受的 flush 值.

* `zlib.constants.Z_NO_FLUSH`
* `zlib.constants.Z_PARTIAL_FLUSH`
* `zlib.constants.Z_SYNC_FLUSH`
* `zlib.constants.Z_FULL_FLUSH`
* `zlib.constants.Z_FINISH`
* `zlib.constants.Z_BLOCK`
* `zlib.constants.Z_TREES`

返回压缩/解压函数的返回值. 发送错误时为负值, 正值用于特殊但正常的事件.

* `zlib.constants.Z_OK`
* `zlib.constants.Z_STREAM_END`
* `zlib.constants.Z_NEED_DICT`
* `zlib.constants.Z_ERRNO`
* `zlib.constants.Z_STREAM_ERROR`
* `zlib.constants.Z_DATA_ERROR`
* `zlib.constants.Z_MEM_ERROR`
* `zlib.constants.Z_BUF_ERROR`
* `zlib.constants.Z_VERSION_ERROR`

压缩等级.

* `zlib.constants.Z_NO_COMPRESSION`
* `zlib.constants.Z_BEST_SPEED`
* `zlib.constants.Z_BEST_COMPRESSION`
* `zlib.constants.Z_DEFAULT_COMPRESSION`

压缩策略

* `zlib.constants.Z_FILTERED`
* `zlib.constants.Z_HUFFMAN_ONLY`
* `zlib.constants.Z_RLE`
* `zlib.constants.Z_FIXED`
* `zlib.constants.Z_DEFAULT_STRATEGY`

