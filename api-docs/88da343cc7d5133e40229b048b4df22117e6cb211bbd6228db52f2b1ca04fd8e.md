<!-- YAML
added: v0.9.12
-->

* `msecs` {number}
* `callback` {Function}
* 返回: {http.ServerResponse}

将套接字的超时值设置为 `msecs`。 
如果提供了回调，则会将其作为监听器添加到响应对象上的 `'timeout'` 事件中。

如果没有 `'timeout'` 监听器添加到请求、响应、或服务器，则套接字在超时时将被销毁。 
如果有回调处理函数分配给请求、响应、或服务器的 `'timeout'` 事件，则必须显式处理超时的套接字。


