<!-- YAML
added: v0.1.27
-->
* `hostname` {string}
* `callback` {Function}
  - `err` {Error}
  - `addresses` {Object[]}

使用 DNS 协议为 `hostname` 解析服务记录（`SRV` 记录）。
传给 `callback` 函数的 `addresses` 参数将会是一个具有以下属性的对象数组：

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

