<!-- YAML
added: v0.3.2
-->
- `hostname` {string}
- `callback` {Function}
  - `err` {Error}
  - `addresses` {string[]}

使用`DNS`协议解析`CNAME`记录主机名。`adresses`参数是传递给`callback`函数规范内有效的主机名数组（例如：`['bar.example.com']`）.

