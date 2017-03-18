<!-- YAML
added: v0.1.90
-->

在不活动的socket`timeout`几毫秒之后，设置socket为超时。
默认，`net.Socket`没有超时。

当一个空闲的超时被触发时，socket将收到[`'timeout'`][]事件，但是连接并不会停止。
用户必须手动的[`end()`][]或者[`destroy()`][]这个socket。

如果`timeout`的值为0，那么存在的空闲的超时将被禁止。


可选的`callback`参数将被添加为[`'timeout'`][]事件的一次行监听器。

返回`socket`.

