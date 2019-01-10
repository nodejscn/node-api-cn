<!-- YAML
added: v8.2.0
-->

* {integer}  单个 `Buffer` 实例允许的最大内存。

在 32 位的架构上，该值是 `(2^30)-1`（1 GB）。
在 64 位的架构上，该值是 `(2^31)-1`（2 GB）。

也可使用 [`buffer.kMaxLength`]。

