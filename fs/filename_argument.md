
<!--type=misc-->

仅在 Linux、macOS、Windows 和 AIX 上支持在回调中提供 `filename` 参数。 
即使在支持的平台上，也不总是保证提供 `filename`。 
因此，不要假设在回调中始终提供 `filename` 参数，并且如果它为 `null` 则需要一些后备逻辑。

```js
fs.watch('somedir', (eventType, filename) => {
  console.log(`事件类型是: ${eventType}`);
  if (filename) {
    console.log(`提供的文件名: ${filename}`);
  } else {
    console.log('文件名未提供');
  }
});
```

