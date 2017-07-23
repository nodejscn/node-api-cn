<!-- YAML
added: v0.6.0
-->

* Returns: {Object}

`os.networkInterfaces()`方法返回一个对象,包含只有被赋予网络地址的网络接口. 

在返回对象的每个关键词都指明了一个网络接口.

返回的值是一个对象数组, 每个都描述了赋予的网络地址.

被赋予网络地址的对象包含的属性:

* `address` {string} 被赋予的 IPv4 或 IPv6 地址
* `netmask` {string}  IPv4 或 IPv6 子网掩码
* `family` {string}  `IPv4` 或 `IPv6`
* `mac` {string} 网络接口的MAC地址
* `internal` {boolean} 如果 网络接口是loopback或相似的远程不能用的接口时,
值为`true`,否则为`false`
* `scopeid` {number} IPv6 数字领域识别码 (只有当 `family`
是`IPv6`时可用)

<!-- eslint-skip -->
```js
{
  lo: [
    {
      address: '127.0.0.1',
      netmask: '255.0.0.0',
      family: 'IPv4',
      mac: '00:00:00:00:00:00',
      internal: true
    },
    {
      address: '::1',
      netmask: 'ffff:ffff:ffff:ffff:ffff:ffff:ffff:ffff',
      family: 'IPv6',
      mac: '00:00:00:00:00:00',
      internal: true
    }
  ],
  eth0: [
    {
      address: '192.168.1.108',
      netmask: '255.255.255.0',
      family: 'IPv4',
      mac: '01:02:03:0a:0b:0c',
      internal: false
    },
    {
      address: 'fe80::a00:27ff:fe4e:66a1',
      netmask: 'ffff:ffff:ffff:ffff::',
      family: 'IPv6',
      mac: '01:02:03:0a:0b:0c',
      internal: false
    }
  ]
}
```

