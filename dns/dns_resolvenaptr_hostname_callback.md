<!-- YAML
added: v0.9.12
-->
- `hostname` {string}
- `callback` {Function}
  - `err` {Error}
  - `addresses` {Object[]}

使用DNS协议来处理基于正则表达式匹配的记录(`NAPTR`记录)的主机名。`adresses`参数是传递给`callback`函数的主机名对象数组，对象包含属性：

* `flags`
* `service`
* `regexp`
* `replacement`
* `order`
* `preference`

例如：

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

