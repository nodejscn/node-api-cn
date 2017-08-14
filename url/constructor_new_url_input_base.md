
* `input` {string} 要解析的输入URL
* `base` {string|URL} 如果“input”是相对URL，则为要解析的基本URL。

通过将`input`解析到`base`上创建一个新的`URL`对象。如果`base`是一个字符串，则解析方法与`new URL(base)`相同。


```js
const { URL } = require('url');
const myURL = new URL('/foo', 'https://example.org/');
  // https://example.org/foo
```

如果`input`或`base`是无效URLs，将会抛出`TypeError`。请注意给定值将被强制转换为字符串。例如：


```js
const { URL } = require('url');
const myURL = new URL({ toString: () => 'https://example.org/' });
  // https://example.org/
```

存在于`input`主机名中的Unicode字符将被使用[Punycode][]算法自动转换为ASCII。

```js
const { URL } = require('url');
const myURL = new URL('https://你好你好');
  // https://xn--6qqa088eba/
```

*Note*: This feature is only available if the `node` executable was compiled
with [ICU][] enabled. If not, the domain names are passed through unchanged.
