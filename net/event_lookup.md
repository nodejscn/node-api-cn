<!-- YAML
added: v0.11.3
-->

在解析域名之后，进行连接之前被触发。 
不能用于UNIX sockets. 

* `err` {Error|Null} 错误对象.  查看 [`dns.lookup()`][].
* `address` {String} IP地址.
* `family` {String|Null} IP地址类型.  See [`dns.lookup()`][].
* `host` {String} 域名.

