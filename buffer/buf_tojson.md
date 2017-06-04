<!-- YAML
added: v0.9.2
-->

* 返回: {Object}

返回 `buf` 的 JSON 格式。
当字符串化一个 `Buffer` 实例时，[`JSON.stringify()`] 会隐式地调用该函数。

例子：

```js
const buf = Buffer.from([0x1, 0x2, 0x3, 0x4, 0x5]);
const json = JSON.stringify(buf);

// 输出: {"type":"Buffer","data":[1,2,3,4,5]}
console.log(json);

const copy = JSON.parse(json, (key, value) => {
  return value && value.type === 'Buffer' ?
    Buffer.from(value.data) :
    value;
});

// 输出: <Buffer 01 02 03 04 05>
console.log(copy);
```

