
我们可以使用 `Readable.from()` 实用方法从异步生成器构造 Node.js 可读流：


```js
const { Readable } = require('stream');

async function * generate() {
  yield 'a';
  yield 'b';
  yield 'c';
}

const readable = Readable.from(generate());

readable.on('data', (chunk) => {
  console.log(chunk);
});
```

