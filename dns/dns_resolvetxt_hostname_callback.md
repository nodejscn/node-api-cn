<!-- YAML
added: v0.1.27
-->
- `hostname` {string}
- `callback` {Function}
  - `err` {Error}
  - `addresses` {string[]}

使用DNS协议处理文本查询主机名(TXT记录)。回调函数`callback`会返回`addresses`参数，它是一个文本记录与主机名一一对应的二维数组(例如：`[ ['v=spf1 ip4:0.0.0.0 ', '~all' ] ]`).
每个数组文本块包含一条记录。根据用例,这些可以是连接在一起或单独对待。
