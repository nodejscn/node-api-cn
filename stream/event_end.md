<!-- YAML
added: v0.9.4
-->

`'end'` 事件将在流中再没有数据可供消费时触发。

*注意*： `'end'` 事件只有在数据被完全消费后 **才会触发** 。 可以在数据被完全消费后，通过将流转换到 
flowing 模式， 或反复调用 [`stream.read()`][stream-read] 方法来实现这一点。

```js
const readable = getReadableStreamSomehow();
readable.on('data', (chunk) => {
  console.log(`Received ${chunk.length} bytes of data.`);
});
readable.on('end', () => {
  console.log('There will be no more data.');
});
```

