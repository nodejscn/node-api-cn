<!-- YAML
added: v0.6.0
-->

* 返回: {Object}

返回一个对象，该对象包含已分配了网络地址的网络接口。

返回的对象上的每个键都标识了一个网络接口。
关联的值是一个对象数组，每个对象描述了一个分配的网络地址。

分配的网络地址的对象上可用的属性包括：

* `address` {string} 分配的 IPv4 或 IPv6 地址。
* `netmask` {string}  IPv4 或 IPv6 的子网掩码。
* `family` {string}  `IPv4` 或 `IPv6`。
* `mac` {string} 网络接口的 MAC 地址。
* `internal` {boolean} 如果网络接口是不可远程访问的环回接口或类似接口，则为 `true`，否则为 `false`。
* `scopeid` {number} 数值型的 IPv6 作用域 ID（仅当 `family` 为 `IPv6` 时指定）。
* `cidr` {string} 以 CIDR 表示法分配的带有路由前缀的 IPv4 或 IPv6 地址。如果 `netmask` 无效，则此属性会被设为 `null`。

<!-- eslint-skip -->
```js
{
  lo: [
    {
      address: '127.0.0.1',
      netmask: '255.0.0.0',
      family: 'IPv4',
      mac: '00:00:00:00:00:00',
      internal: true,
      cidr: '127.0.0.1/8'
    },
    {
      address: '::1',
      netmask: 'ffff:ffff:ffff:ffff:ffff:ffff:ffff:ffff',
      family: 'IPv6',
      mac: '00:00:00:00:00:00',
      scopeid: 0,
      internal: true,
      cidr: '::1/128'
    }
  ],
  eth0: [
    {
      address: '192.168.1.108',
      netmask: '255.255.255.0',
      family: 'IPv4',
      mac: '01:02:03:0a:0b:0c',
      internal: false,
      cidr: '192.168.1.108/24'
    },
    {
      address: 'fe80::a00:27ff:fe4e:66a1',
      netmask: 'ffff:ffff:ffff:ffff::',
      family: 'IPv6',
      mac: '01:02:03:0a:0b:0c',
      scopeid: 1,
      internal: false,
      cidr: 'fe80::a00:27ff:fe4e:66a1/64'
    }
  ]
}
```

