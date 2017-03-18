<!-- YAML
added: v0.1.90
-->

一个生成器函数，返回一个新的 Unix [`net.Socket`][] 并且自动的
连接到所提供的`path`参数.

`connectListener`参数将一次被用作监听器来监听[`'connect'`][]事件。


