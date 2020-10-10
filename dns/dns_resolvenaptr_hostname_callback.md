<!-- YAML
added: v0.9.12
-->
* `hostname` {string}
* `callback` {Function}
  - `err` {Error}
  - `addresses` {Object[]}

使用 DNS 协议为 `hostname` 解析基于正则表达式的记录（`NAPTR` 记录）。
传给 `callback` 函数的 `adresses` 参数将会包含具有以下属性的对象数组：

* `flags`
* `service`
* `regexp`
* `replacement`
* `order`
* `preference`

<!-- eslint-skip -->
```js
{
  flags: 's',
  service: 'SIP+D2U',
  regexp: '',
  replacement: '_sip._udp.example.com',
  order: 30,
  preference: 100
}
```

