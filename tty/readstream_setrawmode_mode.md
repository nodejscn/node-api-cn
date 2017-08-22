<!-- YAML
added: v0.7.7
-->

把 `tty.ReadStream` 配置成原始模式。

在原始模式中，输入按字符逐个生效，但不包括修饰符。
终端对字符的所有特殊处理会被禁用，包括应答输入的字符。
该模式中 `CTRL`+`C` 不再产生 `SIGINT`。

* `mode` {boolean} 如果为 `true`，则把 `tty.ReadStream` 配置成原始模式。
  如果为 `false`，则把 `tty.ReadStream` 配置成默认模式。
  `readStream.isRaw` 属性会被设为对应的值。

