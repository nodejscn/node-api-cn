<!-- YAML
added: v3.0.0
-->

* {integer} 分配给单个 `Buffer` 实例的最大内存

在32位架构上，该值为 `(2^30)-1` (~1GB)。
在64位架构上，该值为 `(2^31)-1` (~2GB)。

注意整个属性是通过 `require('buffer')` 返回的 `buffer` 模块的属性，而不是全局 `Buffer` 对象或 `Buffer` 实例的属性。
