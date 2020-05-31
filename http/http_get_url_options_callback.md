<!-- YAML
added: v0.3.6
changes:
  - version: v10.9.0
    pr-url: https://github.com/nodejs/node/pull/21616
    description: 参数 `url` 可以与单独的 `options` 对象一起传入。
  - version: v7.5.0
    pr-url: https://github.com/nodejs/node/pull/10638
    description: 参数 `options` 可以是 WHATWG `URL` 对象。
-->

* `url` {string | URL}
* `options` {Object} 接受与 [`http.request()`] 相同的 `options`，但是 `method` 始终被设置为 `GET`。
  从原型继承的属性会被忽略。
* `callback` {Function}
* 返回: {http.ClientRequest}

由于大多数请求都是不带请求体的 GET 请求，因此 Node.js 提供了这个便捷的方法。
这个方法与 [`http.request()`] 唯一的区别是，它将请求方法设置为 GET 并且会自动调用 `req.end()`。
由于 [`http.ClientRequest`] 章节中所述的原因，回调必须要消费响应的数据。

`callback` 调用时只有一个参数，该参数是 [`http.IncomingMessage`] 的实例。

获取 JSON 的示例：

```js
http.get('http://nodejs.org/dist/index.json', (res) => {
  const { statusCode } = res;
  const contentType = res.headers['content-type'];

  let error;
  if (statusCode !== 200) {
    error = new Error('请求失败\n' +
                      `状态码: ${statusCode}`);
  } else if (!/^application\/json/.test(contentType)) {
    error = new Error('无效的 content-type.\n' +
                      `期望的是 application/json 但接收到的是 ${contentType}`);
  }
  if (error) {
    console.error(error.message);
    // 消费响应的数据来释放内存。
    res.resume();
    return;
  }

  res.setEncoding('utf8');
  let rawData = '';
  res.on('data', (chunk) => { rawData += chunk; });
  res.on('end', () => {
    try {
      const parsedData = JSON.parse(rawData);
      console.log(parsedData);
    } catch (e) {
      console.error(e.message);
    }
  });
}).on('error', (e) => {
  console.error(`出现错误: ${e.message}`);
});
```

