<!-- YAML
added: v0.9.2
-->

* 返回: {Object}

返回 `buf` 的 JSON 格式。
当字符串化 `Buffer` 实例时，[`JSON.stringify()`] 会调用该函数。

`Buffer.from()` 接受此方法返回的格式的对象。 
特别是，`Buffer.from(buf.toJSON())` 的工作方式类似于 `Buffer.from(buf)`。

```js
const buf = Buffer.from([0x1, 0x2, 0x3, 0x4, 0x5]);
const json = JSON.stringify(buf);

console.log(json);
// 打印: {"type":"Buffer","data":[1,2,3,4,5]}

const copy = JSON.parse(json, (key, value) => {
  return value && value.type === 'Buffer' ?
    Buffer.from(value) :
    value;
});

console.log(copy);
// 打印: <Buffer 01 02 03 04 05>
```

