<!-- YAML
added: v0.3.6
changes:
  - version: v10.9.0
    pr-url: https://github.com/nodejs/node/pull/21616
    description: The `url` parameter can now be passed along with a separate
                 `options` object.
  - version: v7.5.0
    pr-url: https://github.com/nodejs/node/pull/10638
    description: The `options` parameter can be a WHATWG `URL` object.
-->

* `url` {string | URL}
* `options` {Object} 同 [`http.request()`] 的 `options`，但 `method` 会被设为 `GET`。
* `callback` {Function}
* 返回: {http.ClientRequest}

因为大多数请求都是 GET 请求且不带请求主体，所以 Node.js 提供了便捷的方法。
与 [`http.request()`] 的区别是，请求的方法是 GET 且自动调用 `req.end()`。

`callback` 只有一个参数 `res`，`res` 是一个 [`http.IncomingMessage`] 实例。

例子，获取 JSON：

```js
http.get('http://nodejs.cn/index.json', (res) => {
  const { statusCode } = res;
  const contentType = res.headers['content-type'];

  let error;
  if (statusCode !== 200) {
    error = new Error('请求失败\n' +
                      `状态码: ${statusCode}`);
  } else if (!/^application\/json/.test(contentType)) {
    error = new Error('非法的 content-type.\n' +
                      `期望的是 application/json 但接收到的是 ${contentType}`);
  }
  if (error) {
    console.error(error.message);
    // 消费响应的数据以释放内存。
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
  console.error(`报错: ${e.message}`);
});
```

