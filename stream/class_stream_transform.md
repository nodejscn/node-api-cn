<!-- YAML
added: v0.9.4
-->

<!--type=class-->

转换流（Transform）是一种 [`Duplex`] 流，但它的输出与输入是相关联的。
与 [`Duplex`] 流一样，`Transform` 流也同时实现了 [`Readable`] 和 [`Writable`] 接口。

`Transform` 流的例子包括：

* [zlib 流][zlib]
* [crypto 流][crypto]


