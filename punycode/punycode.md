<!-- YAML
changes:
  - version: v7.0.0
    pr-url: https://github.com/nodejs/node/pull/7941
    description: Accessing this module will now emit a deprecation warning.
-->

> 稳定性: 0 - 废弃的

**Node.js中捆绑的punycode模块的版本已被弃用**。在之后主要版本的Node.js中，此模块将被删除。当前使用`punycode`模块的用户应该使用用户空间提供的[Punycode.js][]模块来做替换。

`punycode`模块是[Punycode.js][]模块的绑定版本。可以通过以下方式使用它：

```js
const punycode = require('punycode');
```

[Punycode][]是由RFC 3492定义的主要用于国际化域名的字符编码方案。因为URL中主机名限制只能是ASCII字符，包括非ASCII字符的主机名必须使用Punycode算法转化为ASCII。例如，将汉字转化为英文单词，`'example'`对应`'例'`。国际化域名后，`'例.com'`(等同于`'example.com'`)将被Punycode算法转化为ASCII字符串`'xn--fsq.com'`。

`punycode`模块提供了Punycode标准的简单实现。

*请注意*: Node.js使用的`punycode`模块是第三方依赖关系，仅为开发人员提供方便。对模块进行修复或其他修改必须指向[Punycode.js][]项目。

