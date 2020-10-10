
```js
(async function() {
  for await (const chunk of readable) {
    console.log(chunk);
  }
})();
```

异步迭代器在流上注册一个永久的错误处理程序，以防止任何未处理的 post-destroy 错误。

