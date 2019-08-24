
* {string}

获取及设置 URL 的端口部分。

端口值可以是数字或包含 `0` 到 `65535`（含）范围内的数字字符串。 
将值设置为给定 `protocol` 的 `URL` 对象的默认端口将会导致 `port` 值变为空字符串（`''`）。

端口值可以是空字符串，在这种情况下，端口取决于协议/规范：

| 协议 | 端口 |
| :------- | :--- |
| "ftp"    | 21   |
| "file"   |      |
| "gopher" | 70   |
| "http"   | 80   |
| "https"  | 443  |
| "ws"     | 80   |
| "wss"    | 443  |

在为端口分配值后，将首先使用 `.toString()` 将值转换为字符串。

如果该字符串无效但以数字开头，则将前导号码分配给 `port`。 
如果数字位于上述范围之外，则忽略它。

```js
const myURL = new URL('https://example.org:8888');
console.log(myURL.port);
// 打印 8888

// 默认端口将自动转换为空字符。
// (HTTPS 协议默认端口是 443)
myURL.port = '443';
console.log(myURL.port);
// 打印空字符
console.log(myURL.href);
// 打印 https://example.org/

myURL.port = 1234;
console.log(myURL.port);
// 打印 1234
console.log(myURL.href);
// 输出 https://example.org:1234/

// 完全无效的端口字符串将被忽略。
myURL.port = 'abcd';
console.log(myURL.port);
// 打印 1234

// 开头的数字将会被当做端口号。
myURL.port = '5678abcd';
console.log(myURL.port);
// 打印 5678

// 非整形数字将会被截断。
myURL.port = 1234.5678;
console.log(myURL.port);
// 打印 1234

// 超出范围的数字将被忽略。
myURL.port = 1e10; // 10000000000，将按如下所述进行范围检查。
console.log(myURL.port);
// 打印 1234
```

包含小数点的数字（例如浮点数或科学计数法中的数字）不是此规则的例外。 
假设它们有效，将小数点前的前导数字设置为 URL 的端口：

```js
myURL.port = 4.567e21;
console.log(myURL.port);
// 打印 4 (因为它是字符串 '4.567e21' 中的前导数字)
```

