
[WHATWG URL 标准][WHATWG URL Standard]认为少数 URL 协议规范在解析和序列化方面具有特殊性。 
使用这些特殊协议之一解析 URL 时，`url.protocol` 属性可能会被更改为其他特殊协议，但不能更改为非特殊协议，反之亦然。

例如，从 `http` 更改为 `https` 工作如下：

```js
const u = new URL('http://example.org');
u.protocol = 'https';
console.log(u.href);
// https://example.org
```

但是，从 `http` 更改为假设的 `fish` 议并不是因为新协议并不特殊。

```js
const u = new URL('http://example.org');
u.protocol = 'fish';
console.log(u.href);
// http://example.org
```

同样，也不允许从非特殊协议更改为特殊协议：

```js
const u = new URL('fish://example.org');
u.protocol = 'http';
console.log(u.href);
// fish://example.org
```

根据 WHATWG URL 标准，特殊协议规范是 `ftp`、`file`、`gopher`、`http`、`https`、`ws` 和 `wss`。

