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
* `options` {Object} 接受与 [`http.request()`] 相同的 `options`，且 `method` 始终设置为 `GET`。从原型继承的属性将被忽略。
* `callback` {Function}
* 返回: {http.ClientRequest}

由于大多数请求都是没有主体的 GET 请求，因此 Node.js 提供了这个便捷的方法。
这个方法与 [`http.request()`] 的唯一区别是它将方法设置为 GET 并自动调用 `req.end()`。
注意，由于 [`http.ClientRequest`] 章节中所述的原因，回调必须注意消费响应数据。

`callback` 调用时只有一个参数，该参数是 [`http.IncomingMessage`] 的实例。

获取 JSON 的示例：

```js
http.get('http://nodejs.cn/index.json', (res) => {
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
    // 消费响应数据来释放内存。
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

