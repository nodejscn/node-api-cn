<!-- YAML
added: v10.6.0
-->

* `hostname` {string} 要解析的主机名。
* `options` {Object}
  * `ttl` {boolean} 检索每个记录的生存时间值（TTL）。
  如果为`true`，则使用数组`{ address: '1.2.3.4', ttl: 60 }`对象而不是字符串数组来解析`Promise`，而TTL以秒表示。
  
  
  Retrieve the Time-To-Live value (TTL) of each record.
    When `true`, the `Promise` is resolved with an array of
    `{ address: '1.2.3.4', ttl: 60 }` objects rather than an array of strings,
    with the TTL expressed in seconds.
    
使用DNS协议为以下地址解析IPv4地址（`A` 记录）主机名。
成功后，将通过一系列IPv4解决`Promise`地址（比如，`['74.125.79.104', '74.125.79.105', '74.125.79.106']`）
