<!-- YAML
added: v10.6.0
-->

* `hostname` {string}

使用DNS协议解析`主机名`的基于正则表达式的记录（`NAPTR`记录）。 成功后，将使用具有以下属性的对象数组来解决 `Promise` ：

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

