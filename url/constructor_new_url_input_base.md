
* `input` {string} 要解析的绝对或相对的 URL。如果 `input` 是相对路径，则需要 `base`。 如果 `input` 是绝对路径，则忽略 `base`。
* `base` {string|URL} 如果 `input` 不是绝对路径，则为要解析的基本 URL。

通过将 `input` 相对于 `base` 进行解析，创建一个新的 `URL` 对象。
如果 `base` 是一个字符串，则解析方法与 `new URL(base)` 相同。


```js
const myURL = new URL('/foo', 'https://example.org/');
// https://example.org/foo
```

如果 `input` 或 `base` 是无效的 URL，则将会抛出 `TypeError`。
注意，给定值将会被强制转换为字符串。
例如：


```js
const myURL = new URL({ toString: () => 'https://example.org/' });
// https://example.org/
```

存在于 `input` 主机名中的 Unicode 字符将被使用 [Punycode] 算法自动转换为 ASCII。

```js
const myURL = new URL('https://測試');
// https://xn--g6w251d/
```

只有在启用 [ICU] 的情况下编译 `node` 可执行文件时，此功能才可用。 
如果没有，则域名将保持不变。

如果 `input` 是绝对的 URL 并且提供了 `base`，则事先不知道它，建议验证 `URL` 对象的 `origin` 是否是预期的。

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

