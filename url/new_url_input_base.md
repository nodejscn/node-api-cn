
* `input` {string} 要解析的绝对或相对的输入 URL。
   如果 `input` 是相对的，则 `base` 是必需的。 
   如果 `input` 是绝对的，则 `base` 是忽略的。
* `base` {string|URL} 如果 `input` 不是绝对的时要解析的基本 URL。

通过相对于 `base` 解析 `input`，创建一个新的 `URL` 对象。
如果 `base` 被作为一个字符串传入，则它会被解析为等效于 `new URL(base)`。


```js
const myURL = new URL('/foo', 'https://example.org/');
// https://example.org/foo
```

URL 构造器可被作为全局对象上的一个属性访问。
它也可以被从内置的 url 模块导入：


```js
console.log(URL === require('url').URL); // 打印 'true'。
```

如果 `input` 或者 `base` 是无效的 URL，则一个 `TypeError` 会被抛出。
注意，给定的值会被强制转换为字符串。
例如：


```js
const myURL = new URL({ toString: () => 'https://example.org/' });
// https://example.org/
```

`input` 的主机名中出现的 Unicode 字符会被使用 [Punycode] 算法自动地转换为 ASCII。

```js
const myURL = new URL('https://測試');
// https://xn--g6w251d/
```

此特性只有在 `node` 可执行文件在 [ICU] 被启用的情况下被编译时才可用。 
如果不是，则域名被原样传入。

如果事先不知道 `input` 是一个绝对的 URL 并且一个 `base` 被提供，则建议校验 `URL` 对象的 `origin` 是否是期望的。

```js
let myURL = new URL('http://Example.com/', 'https://example.org/');
// http://example.com/

myURL = new URL('https://Example.com/', 'https://example.org/');
// https://example.com/

myURL = new URL('foo://Example.com/', 'https://example.org/');
// foo://Example.com/

myURL = new URL('http:Example.com/', 'https://example.org/');
// http://example.com/

myURL = new URL('https:Example.com/', 'https://example.org/');
// https://example.org/Example.com/

myURL = new URL('foo:Example.com/', 'https://example.org/');
// foo:Example.com/
```

