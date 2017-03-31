<!-- YAML
added: v0.11.4
-->

* `options` {Object} 一个提供名称生成信息的选项的集合
  * `host` {String} 请求发送至的服务器的域名或 IP 地址
  * `port` {Number} 远程服务器的端口
  * `localAddress` {String} 当发送请求时，要绑定到网络连接的本地接口
* 返回: {String}

获取请求选项集合的唯一名称，以确定连接是否可以再利用。
对于一个 HTTP 代理，这会返回 `host:port:localAddress`。
对于一个 HTTPS 代理，名称会包括 CA、证书、密码和其他 HTTPS/TLS-specific 选项，以确定 socket 的可复用性。

