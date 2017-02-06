<!-- YAML
added: v0.11.6
-->

* {Array}

接收到的原始请求/响应头列表。

注意，键和值是在同一列表中。
它**不是**一个元组列表。
所以，偶数偏移量为键，奇数偏移量为对应的值。

报头名称没有转换为小写，也没有合并去重。

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

