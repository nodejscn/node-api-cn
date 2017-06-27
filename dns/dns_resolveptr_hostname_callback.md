<!-- YAML
added: v6.0.0
-->
- `hostname` {string}
- `callback` {Function}
  - `err` {Error}
  - `addresses` {string[]}

使用DNS协议处理主机名引用记录(PTR记录)。`addresses`参数将一个字符串数组传递给回调函数`callback`,其中包含回复记录。

