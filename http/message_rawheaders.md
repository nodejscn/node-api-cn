<!-- YAML
added: v0.11.6
-->

* {Array}

接收到的原始的请求头或响应头列表。

注意，键和值在同一个列表中。
偶数位的是键，奇数位的是对应的值。

头信息的名称不会被转换为小写，重复的也不会被合并。

```js
// 输出类似以下的东西：
//
// [ 'user-agent',
//   'this is invalid because there can be only one',
//   'User-Agent',
//   'curl/7.22.0',
//   'Host',
//   '127.0.0.1:8000',
//   'ACCEPT',
//   '*/*' ]
console.log(request.rawHeaders);
```

