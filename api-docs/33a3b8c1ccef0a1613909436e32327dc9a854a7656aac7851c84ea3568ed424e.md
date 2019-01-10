<!-- YAML
added: v0.1.27
-->
- `hostname` {string}
- `callback` {Function}
  - `err` {Error}
  - `addresses` {Object[]}

使用DNS协议处理邮件交换记录主机名(`MX`记录)。`adresses`参数是传递给`callback`函数的主机名对象数组，对象包含`priority`和`exchange`属性（例如： `[{priority: 10, exchange: 'mx.example.com'}, ...]`）。

