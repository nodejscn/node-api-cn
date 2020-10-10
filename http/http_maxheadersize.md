<!-- YAML
added:
 - v11.6.0
 - v10.15.0
-->

* {number}

只读属性，指定 HTTP 消息头的最大允许大小（以字节为单位）。 
默认为 8KB。 
可使用 [`--max-http-header-size`] 命令行选项进行配置。

通过传入 `maxHeaderSize` 选项，可以为服务器和客户端的请求重写此值。

