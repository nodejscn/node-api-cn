<!-- YAML
added: v0.7.7
-->

允许配置 `tty.ReadStream` 作为一个原始设备来操作。

当在原始模式中，输入总是按字符生效，但不包括修饰符。
此外，终端对字符的所有特殊处理会被禁用，包括应答输入的字符。
注意，该模式中 `CTRL`+`C` 不再产生一个 `SIGINT`。

* `mode` {boolean} 如果为 `true`，则配置 `tty.ReadStream` 作为一个原始设备来操作。
  如果为 `false`，则配置 `tty.ReadStream` 以默认模式来操作。
  `readStream.isRaw` 属性会被设为对应的值。

