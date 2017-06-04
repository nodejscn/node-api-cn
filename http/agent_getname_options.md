<!-- YAML
added: v0.11.4
-->

* `options` {Object} 为名称生成程序提供信息的选项。
  * `host` {string} 请求发送至的服务器的域名或 IP 地址。
  * `port` {number} 远程服务器的端口。
  * `localAddress` {string} 当发送请求时，为网络连接绑定的本地接口。
* 返回: {string}

为请求选项的集合获取一个唯一的名称，用来判断一个连接是否可以被复用。
对于 HTTP 代理，返回 `host:port:localAddress`。
对于 HTTPS 代理，名称会包含 CA、证书、密码、以及其他 HTTPS/TLS 特有的用于判断 socket 复用性的选项。

