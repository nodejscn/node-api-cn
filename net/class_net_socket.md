<!-- YAML
added: v0.3.4
-->

这个对象是TCP或者本地socket的一个抽象。`net.Socket`实例实现了
一个双工流接口。它们可以由用户创建用于客户端（和[`connect()`][]），
或者是由Node.js创建，用于通过一个服务器的`'connection'`事件传参给用户。


