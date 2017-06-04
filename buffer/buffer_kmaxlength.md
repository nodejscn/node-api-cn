<!-- YAML
added: v3.0.0
-->

* {integer} 分配给单个 `Buffer` 实例的最大内存

在32位架构上，该值为 `(2^30)-1` (~1GB)。
在64位架构上，该值为 `(2^31)-1` (~2GB)。

Note that this is a property on the `buffer` module returned by
`require('buffer')`, not on the `Buffer` global or a `Buffer` instance.

