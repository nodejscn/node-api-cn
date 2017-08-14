
[WHATWG URL Standard][]使用比遗留的API更具选择性和更精细的方法来选择使用的编码字符。

WHATWG算法定义了三个“百分比编码集”，它们描述了必须进行百分编码的字符范围：

* *C0 control percent-encode set(C0控制百分比编码集)* 包括范围在U+0000 ~ U+001F（含）的代码点及大于U+007E的所有代码点。

* *path percent-encode set(路径百分比编码集)* 包括 *C0 control percent-encode set(C0控制百分比编码集)* 的代码点 及 U+0020, U+0022, U+0023, U+003C, U+003E, U+003F, U+0060, U+007B, 和 U+007D 的代码点。

* *userinfo encode set(用户信息编码集)* 包括 *path percent-encode set(路径百分比编码集)* 的代码点 及 U+002F, U+003A, U+003B, U+003D, U+0040, U+005B, U+005C, U+005D, U+005E, 和 U+007C 的代码点。

*userinfo percent-encode set(用户信息百分比编码集)* 专门用于用户名和密码部分的编码。*path percent-encode set(路径百分比编码集)* 用于大多数URL的路径部分编码。*C0 control percent-encode set(C0控制百分比编码集)* 则用于所有其他情况的编码，特别地包括URL的分段部分，特殊条件下也包括主机及路径部分。

当主机名中出现非ASCII字符时，主机名将使用[Punycode][]算法进行编码。然而，请注意，主机名*可能同时* 包含Punycode编码和百分比编码的字符。例如：

```js
const { URL } = require('url');
const myURL = new URL('https://%CF%80.com/foo');
console.log(myURL.href);
  // 输出 https://xn--1xa.com/foo
console.log(myURL.origin);
  // 输出 https://π.com
```

