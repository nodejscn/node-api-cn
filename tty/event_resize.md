<!-- YAML
added: v0.7.7
-->

当 `writeStream.columns` 属性或 `writeStream.rows` 属性发生变化时触发 `'resize'` 事件。
监听器回调函数没有参数。

```js
process.stdout.on('resize', () => {
  console.log('窗口大小发生变化！');
  console.log(`${process.stdout.columns}x${process.stdout.rows}`);
});
```

