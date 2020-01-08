<!-- YAML
added: v8.3.0
changes:
  - version: v11.0.0
    pr-url: v11.0.0
    description: The class is now available on the global object.
-->

[WHATWG 编码标准][WHATWG Encoding Standard] 的 `TextEncoder` API 的实现。 
`TextEncoder` 的所有实例仅支持 UTF-8 编码。

```js
const encoder = new TextEncoder();
const uint8array = encoder.encode('这是一些数据');
```

`TextEncoder` 类在全局对象上也可用。

