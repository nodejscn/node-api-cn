<!-- YAML
added: v0.7.7
-->

当 `writeStream.columns` 属性或 `writeStream.rows` 属性发生变化时触发 `'resize'` 事件。
监听器回调没有参数传入。

```js
process.stdout.on('resize', () => {
  console.log('屏幕大小已改变！');
  console.log(`${process.stdout.columns}x${process.stdout.rows}`);
});
```

