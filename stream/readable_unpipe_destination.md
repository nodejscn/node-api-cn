<!-- YAML
added: v0.9.4
-->

* `destination` {stream.Writable} 可选的，指定需要分离的目标流

`readable.unpipe()` 方法将之前通过[`stream.pipe()`][]方法绑定的流分离

如果 `destination` 没有传入, 则所有绑定的流都会被分离.

如果传入 `destination`, 但它没有被`pipe()`绑定过，则该方法不作为.

```js
const readable = getReadableStreamSomehow();
const writable = fs.createWriteStream('file.txt');
// All the data from readable goes into 'file.txt',
// but only for the first second
readable.pipe(writable);
setTimeout(() => {
  console.log('Stop writing to file.txt');
  readable.unpipe(writable);
  console.log('Manually close the file stream');
  writable.end();
}, 1000);
```

