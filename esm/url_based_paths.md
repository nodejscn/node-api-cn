
ESM基于[`URL`]语义来解析和缓存。这意味着那些包含特殊字符的文件名，如 `#` 和 `?` 需要进行转义。

如果使用 `import` 来解析一个拥有不同查询或片段的模块，该模块将被加载多次。

```js
import './foo?query=1'; // loads ./foo with query of "?query=1"
import './foo?query=2'; // loads ./foo with query of "?query=2"
```

直到现在，模块只能使用 `file:` 协议来加载。