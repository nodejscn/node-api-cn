<!-- YAML
added: v0.5.10
-->

如果Node.js进程是由IPC channel的方式创建的(see the [Child Process][]，
and [Cluster][] documentation)，当子进程收到父进程的的消息时(消息通过[`childprocess.send()`][]发送），
会触发`'message'`事件。

`'message'`事件监听器的回调函数中被传递的参数如下：
* `message`{Object} 解析的JSON对象，或primitive值
* `sendHandle` {Handle object} 一个[`net.Socket`][] 或 [`net.Server`][]对象，或undefined。


