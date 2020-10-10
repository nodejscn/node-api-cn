<!-- YAML
added: v0.7.7
-->

每当 `writeStream.columns` 或 `writeStream.rows` 属性发生变化时，则触发 `'resize'` 事件。 
当调用时，没有参数传给监听器回调。

```js
process.stdout.on('resize', () => {
  console.log('屏幕大小已改变');
  console.log(`${process.stdout.columns}x${process.stdout.rows}`);
});
```

