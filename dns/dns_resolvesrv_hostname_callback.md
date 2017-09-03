<!-- YAML
added: v0.1.27
-->
- `hostname` {string}
- `callback` {Function}
  - `err` {Error}
  - `addresses` {Object[]}

使用DNS协议来处理主机名服务记录(SRV记录)。`callback`函数返回的`addresses`参数为对象数组,每个对象包含以下属性：

* `priority`
* `weight`
* `port`
* `name`

<!-- eslint-skip -->
```js
{
  priority: 10,
  weight: 5,
  port: 21223,
  name: 'service.example.com'
}
```

