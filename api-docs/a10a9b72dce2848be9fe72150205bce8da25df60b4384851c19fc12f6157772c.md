<!-- YAML
added: v0.11.8
-->

SPKAC 最初是由 Netscape 实现的一种证书签名请求机制, 现在正式成为 [HTML5's `keygen` element][] 的一部分.

`crypto` 模块提供 `Certificate` 类用于处理 SPKAC 数据. 最普遍的用法是处理 HTML5 `keygen` 元素
产生的输出. Node.js 内部使用 [OpenSSL's SPKAC implementation][] 处理.

