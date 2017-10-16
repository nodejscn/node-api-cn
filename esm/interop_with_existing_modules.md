
所有CommonJS，JSON和C++模块都可以通过 `import` 来加载。

以这种方式加载的模块只加载一次，即使 `import` 语句中同一个模块的查询或片段字符串不同。

当通过 `import` 加载时，这些模块将提供一个 `default` 导出相当于完成计算后的 `module.exports` 。

```js
import fs from 'fs';
fs.readFile('./foo.txt', (err, body) => {
  if (err) {
    console.error(err);
  } else {
    console.log(body);
  }
});
```
