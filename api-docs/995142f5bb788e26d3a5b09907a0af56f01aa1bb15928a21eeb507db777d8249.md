<!-- YAML
added: v0.1.5
-->

* {Object}

请求或响应的消息头对象。

消息头的名称和值的键值对。 
消息头的名称都是小写的。

```js
// 打印类似以下：
//
// { 'user-agent': 'curl/7.22.0',
//   host: '127.0.0.1:8000',
//   accept: '*/*' }
console.log(request.headers);
```

原始消息头中的重复项会按以下方式处理，具体取决于消息头的名称：

* 重复的 `age`、`authorization`、`content-length`、`content-type`、
`etag`、`expires`、`from`、`host`、`if-modified-since`、`if-unmodified-since`、 
`last-modified`、`location`、`max-forwards`、`proxy-authorization`、`referer`、
`retry-after` 或 `user-agent` 会被丢弃。
* `set-cookie` 始终是一个数组。重复项都会添加到数组中。
* 对于重复的 `cookie` 消息头，其值会使用与 '; ' 连接到一起。
* 对于所有其他消息头，其值会使用 ', ' 连接到一起。

