<!-- YAML
added: v0.5.9
-->

* `timeout` {number} 请求超时前的毫秒数。
* `callback` {Function} 发生超时时要调用的可选函数。相当于绑定到 `'timeout'` 事件。
* 返回: {http.ClientRequest}

一旦将套接字分配给此请求并且连接了套接字，就会调用 [`socket.setTimeout()`]。


