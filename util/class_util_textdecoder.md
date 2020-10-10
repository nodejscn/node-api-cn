<!-- YAML
added: v8.3.0
-->

[WHATWG 编码标准][WHATWG Encoding Standard]的 `TextDecoder` API 的实现。

```js
const decoder = new TextDecoder('shift_jis');
let string = '';
let buffer;
while (buffer = getNextChunkSomehow()) {
  string += decoder.decode(buffer, { stream: true });
}
string += decoder.decode(); // 流的末尾。
```

