<!-- YAML
added: v0.1.90
-->

* {Error}

当错误出现的时候触发. 不同与 [`net.Socket`][], [`'close'`][]
事件不会在这个事件触发后继续触发 除非
[`server.close()`][] 是手动调用. 在
[`server.listen()`][]中的例子.

