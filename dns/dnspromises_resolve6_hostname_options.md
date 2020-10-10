<!-- YAML
added: v10.6.0
-->

* `hostname` {string} 要解析的主机名。.
* `options` {Object}
  * `ttl` {boolean} 检索每个记录的生存时间值（TTL）。
    如果为true，则使用数组对象`{ address: '0:1:2:3:4:5:6:7', ttl: 60 }`而不是字符串数组来解析`Promise`。 TTL以秒表示。
   
使用DNS协议解析`hostname`的IPv6地址（`AAAA`记录）。 成功后，将使用一系列IPv6地址解析`Promise` 。
