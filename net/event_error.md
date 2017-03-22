<!-- YAML
added: v0.1.90
-->

* {Error}

当错误发生时触发。
不像 [`net.Socket`]，[`'close'`] 事件不会紧接该事件触发，除非 [`server.close()`] 被手动调用。
可在 [`server.listen()`] 的讨论中查看相关例子。

