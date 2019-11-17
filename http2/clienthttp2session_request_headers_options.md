<!-- YAML
added: v8.4.0
-->

* `headers` {HTTP/2 Headers Object}
* `options` {Object}
  * `endStream` {boolean} 如果 `Http2Stream` 可写端初始应该被关闭（例如，当发送不应期望有效载荷主体的 `GET` 请求时），则为 `true`。
  * `exclusive` {boolean} 当为 `true` 且 `parent` 标识一个父流时，则会使创建的流成为父流的唯一直接的依赖，而所有其他现有的依赖会成为新创建的流的依赖。 
     **默认值:** `false`。
  * `parent` {number} 指定新创建的流所依赖的流的数字标识符。
  * `weight` {number} 指定流相对于具有相同 `parent` 的其他流的相对依赖性。 
     该值是一个介于 `1` 到 `256`（含）之间的数字。
  * `waitForTrailers` {boolean} 当为 `true` 时，在发送完最后的 `DATA` 帧之后，`Http2Stream` 将会触发 `'wantTrailers'` 事件。

* 返回: {ClientHttp2Stream}

仅用于 HTTP/2 客户端的 `Http2Session` 实例，`http2session.request()` 会创建并返回一个 `Http2Stream` 实例，该实例可用于将 HTTP/2 请求发送到连接的服务器。

仅当 `http2session.type` 等于 `http2.constants.NGHTTP2_SESSION_CLIENT` 时，此方法才可用。

```js
const http2 = require('http2');
const clientSession = http2.connect('https://localhost:1234');
const {
  HTTP2_HEADER_PATH,
  HTTP2_HEADER_STATUS
} = http2.constants;

const req = clientSession.request({ [HTTP2_HEADER_PATH]: '/' });
req.on('response', (headers) => {
  console.log(headers[HTTP2_HEADER_STATUS]);
  req.on('data', (chunk) => { /* .. */ });
  req.on('end', () => { /* .. */ });
});
```

当设置了 `options.waitForTrailers` 选项时，在排队要发送的最后一块有效载荷数据之后，会立即触发 `'wantTrailers'` 事件。 
然后可以调用 `http2stream.sendTrailers()` 方法将尾部消息头发送到对等方。

当设置了 `options.waitForTrailers` 时，在发送最终的 `DATA` 帧时 `Http2Stream` 将不会自动地关闭。 
用户代码必须调用 `http2stream.sendTrailers()` 或 `http2stream.close()` 来关闭 `Http2Stream`。

`headers` 中未指定 `:method` 和 `:path` 伪消息头，它们分别默认为：

* `:method` = `'GET'`
* `:path` = `/`

