<!-- YAML
added: v0.1.90
-->

当socket连接的另一端发出FIN包时被触发。

默认情况下(`allowHalfOpen == false`)，socket连接一旦将要写完写队列，就会破坏
它的文件描述器。然而，通过设置`allowHalfOpen == true`，socket将不会自动的结束它
这一端，并且允许用户写入任意大小的数据，并且附加说明用户需要手动的调用`end()`在他们那一端。


