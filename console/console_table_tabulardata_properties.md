<!-- YAML
added: v10.0.0
-->

* `tabularData` {any}
* `properties` {string[]} 构造表的备用属性。

尝试使用 `tabularData`（或使用 `properties`）的属性列和 `tabularData` 的行来构造一个表并记录它。
如果无法将其解析为表格，则回退到仅记录参数。


```js
// 这些不能解析为表格数据。
console.table(Symbol());
// Symbol()

console.table(undefined);
// undefined

console.table([{ a: 1, b: 'Y' }, { a: 'Z', b: 2 }]);
// ┌─────────┬─────┬─────┐
// │ (index) │  a  │  b  │
// ├─────────┼─────┼─────┤
// │    0    │  1  │ 'Y' │
// │    1    │ 'Z' │  2  │
// └─────────┴─────┴─────┘

console.table([{ a: 1, b: 'Y' }, { a: 'Z', b: 2 }], ['a']);
// ┌─────────┬─────┐
// │ (index) │  a  │
// ├─────────┼─────┤
// │    0    │  1  │
// │    1    │ 'Z' │
// └─────────┴─────┘
```

