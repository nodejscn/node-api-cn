<!-- YAML
added: v0.11.4
-->

* `options` {Object} 一组选项，为生成名称提供信息。
  * `host` {string} 请求发送至的服务器的域名或 IP 地址。
  * `port` {number} 远程服务器的端口。
  * `localAddress` {string} 为网络连接绑定的本地接口。
  * `family` {integer} 如果不等于 `undefined`，则必须为 4 或 6。
* 返回: {string}

获取一组请求选项的唯一名称，以判定一个连接是否可以被重用。 
对于 HTTP 代理，这返回 `host:port:localAddress` 或 `host:port:localAddress:family`。 
对于 HTTPS 代理，该名称包括 CA、证书、密码、以及其他可判定套接字可重用性的 HTTPS/TLS 特有的选项。

