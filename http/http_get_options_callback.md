<!-- YAML
added: v0.3.6
changes:
  - version: v7.5.0
    pr-url: https://github.com/nodejs/node/pull/10638
    description: The `options` parameter can be a WHATWG `URL` object.
-->

* `options` {Object | string | URL} 接收与[`http.request()`][]相同的设置。
  `method`一直设置为`GET`，忽略继承自原型的属性
* `callback` {Function}
* 返回: {http.ClientRequest}

因为大多数请求都是 GET 请求且不带请求主体，所以 Node.js 提供了该便捷方法。
该方法与 [`http.request()`] 唯一的区别是它设置请求方法为 GET 且自动调用 `req.end()`。
注意，回调函数务必消耗掉响应数据，原因详见 [`http.ClientRequest`] 章节。

`callback` 被调用时只传入一个参数，该参数是 [`http.IncomingMessage`] 的一个实例。

一个获取 JSON 的例子：

```js
http.get('http://nodejs.org/dist/index.json', (res) => {
  const { statusCode } = res;
  const contentType = res.headers['content-type'];

  let error;
  if (statusCode !== 200) {
    error = new Error('请求失败。\n' +
                      `状态码: ${statusCode}`);
  } else if (!/^application\/json/.test(contentType)) {
    error = new Error('无效的 content-type.\n' +
                      `期望 application/json 但获取的是 ${contentType}`);
  }
  if (error) {
    console.error(error.message);
    // 消耗响应数据以释放内存
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
  console.error(`错误: ${e.message}`);
});
```

