
<!--type=misc-->

回调中提供的 `filename` 参数仅在 Linux、macOS、Windows、以及 AIX 系统上支持。
即使在支持的平台中，`filename` 也不能保证提供。
因此，不要以为 `filename` 参数总是在回调中提供，如果它是空的，需要有一定的后备逻辑。

```js
fs.watch('somedir', (eventType, filename) => {
  console.log(`事件类型是: ${eventType}`);
  if (filename) {
    console.log(`提供的文件名: ${filename}`);
  } else {
    console.log('未提供文件名');
  }
});
```

