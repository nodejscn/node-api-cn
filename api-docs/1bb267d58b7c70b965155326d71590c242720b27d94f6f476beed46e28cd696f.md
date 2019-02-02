<!-- YAML
added: v0.7.7
-->

只要 `writeStream.columns` 或 `writeStream.rows` 属性发生更改，就会触发 `'resize'` 事件。 
调用时，没有参数传递给监听器回调。

```js
process.stdout.on('resize', () => {
  console.log('屏幕大小已经改变');
  console.log(`${process.stdout.columns}x${process.stdout.rows}`);
});
```

