
`query` 属性是不含开头 ASCII 问号（`?`）的查询字符串，或一个被 [`querystring`] 模块的 `parse()` 方法返回的对象。
`query` 属性是一个字符串还是一个对象是由传入 `url.parse()` 的 `parseQueryString` 参数决定的。

例如：`'query=string'` or `{'query': 'string'}`

如果返回一个字符串，则不会对查询字符串执行解码。
如果返回一个对象，则键和值都会被解码。

