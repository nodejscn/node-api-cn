<!-- YAML
added: v0.1.5
-->

* {Object}

请求头或响应头的对象。

头信息的名称与值的键值对。
头信息的名称为小写。
例如：

```js
// 输出类似以下的东西：
//
// { 'user-agent': 'curl/7.22.0',
//   host: '127.0.0.1:8000',
//   accept: '*/*' }
console.log(request.headers);
```

原始头信息中的重复数据会按以下方式根据头信息名称进行处理：

* 重复的 `age` 、 `authorization` 、 `content-length` 、 `content-type` 、 
`etag` 、 `expires` 、 `from` 、 `host` 、 `if-modified-since` 、 `if-unmodified-since` 、 
`last-modified` 、 `location` 、 `max-forwards` 、 `proxy-authorization` 、 `referer` 、 
`retry-after` 、或 `user-agent` 会被丢弃。
* `set-cookie` 始终是一个数组。重复的会被添加到数组。
* 对于其他头信息，其值使用 `,` 拼接。

