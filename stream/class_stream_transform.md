<!-- YAML
added: v0.9.4
-->

<!--type=class-->

变换流（Transform streams） 是一种 [Duplex][] 流。它的输出与输入是通过某种方式关联的。和所有 [Duplex][] 流一样，变换流同时实现了 [Readable][] 和 [Writable][] 接口。

变换流的实例包括：

* [zlib streams][zlib]
* [crypto streams][crypto]


