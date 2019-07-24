
* {string}

获取及设置URL的端口(port)部分。

```js
const { URL } = require('url');
const myURL = new URL('https://example.org:8888');
console.log(myURL.port);
  // 输出 8888

// 默认端口将自动转换为空字符
// (HTTPS协议默认端口是443)
myURL.port = '443';
console.log(myURL.port);
  // 输出空字符
console.log(myURL.href);
  // 输出 https://example.org/

myURL.port = 1234;
console.log(myURL.port);
  // 输出 1234
console.log(myURL.href);
  // 输出 https://example.org:1234/

// 完全无效的端口字符串将被忽略
myURL.port = 'abcd';
console.log(myURL.port);
  // 输出 1234

// 开头的数字将会被当做端口数
myURL.port = '5678abcd';
console.log(myURL.port);
  // 输出 5678

// 非整形数字将会被截取部分
myURL.port = 1234.5678;
console.log(myURL.port);
  // 输出 1234

// 超出范围的数字将被忽略
myURL.port = 1e10;
console.log(myURL.port);
  // 输出 1234
```

端口值可以被设置为数字或包含数字的字符串，数字范围`0`~`65535`(包括)。为给定`protocol`的`URL`对象设置端口值将会导致`port`值变成空字符(`''`)。

如果给`port`属性设置的值是无效字符串，但如果字符串以数字开头，那么开头部位的数字将会被赋值给`port`。否则，包括如果数字超出上述要求的数字，将被忽略。


