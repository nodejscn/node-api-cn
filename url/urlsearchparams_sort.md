<!-- YAML
added: v7.7.0
-->

按现有名称就地排列所有的名称-值对。使用[稳定排序算法][]完成排序，因此保留具有相同名称的名称-值对之间的相对顺序。

特别地，该方法可以用来增加缓存命中。
```js
const { URLSearchParams } = require('url');
const params = new URLSearchParams('query[]=abc&type=search&query[]=123');
params.sort();
console.log(params.toString());
  // Prints query%5B%5D=abc&query%5B%5D=123&type=search
```

