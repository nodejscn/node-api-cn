<!-- YAML
added: v0.7.7
-->

* `mode` {boolean} 如果为 `true`，则将 `tty.ReadStream` 配置为作为原始设备运行。 
  如果为 `false`，则将 `tty.ReadStream` 配置为以其默认模式运行。 
  `readStream.isRaw` 属性将会按最终的模式设置。
* 返回: {this} 读取流的实例。

允许配置 `tty.ReadStream`，使其作为原始设备运行。

在原始模式中，输入始终可以逐个字符，但不包括修饰符。 
此外，终端对字符的所有特殊处理都会被禁用，包括回显的输入字符。 
在此模式中，`CTRL`+`C` 将不再产生 `SIGINT`。


