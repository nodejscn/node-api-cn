<!-- YAML
added: v0.1.90
-->
- `hostname` {string}
- `callback` {Function}
  - `err` {Error}
  - `addresses` {string[]}

使用DNS协议处理名称服务器主机名记录(`NS`记录)。`adresses`为有效的名称服务器记录主机名数组（eg:`['ns1.example.com', 'ns2.example.com']`）。

