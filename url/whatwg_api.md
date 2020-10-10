
[WHATWG URL 标志][WHATWG URL Standard]使用比传统的 API 更具选择性和更精细的方法来选择使用的编码字符。

WHATWG 算法定义了四个“百分比编码集”，它们描述了必须进行百分编码的字符范围：

* C0 控制百分比编码集，包括范围在 U+0000 至 U+001F（含）的代码点，以及大于 U+007E 的所有代码点。

* 片段百分比编码集，包括 C0 控制百分比编码集，以及代码点 U+0020、U+0022、U+003C、U+003E 和 U+006。

* 路径百分比编码集，包括 C0 控制百分比编码集，以及代码点 U+0020、U+0022、U+0023、U+003C、U+003E、U+003F、U+0060、U+007B 和 U+007D。

* 用户信息编码集，包括路径百分比编码集，以及代码点 U+002F、U+003A、U+003B、U+003D、U+0040、U+005B、U+005C、U+005D、U+005E 和 U+007C。

用户信息百分比编码集专门用于 URL 中用户名和密码部分的编码。
路径百分比编码集用于大多数 URL 的路径部分编码。
C0 控制百分比编码集则用于所有其他情况的编码，特别包括 URL 的分段部分，特殊条件下也包括主机及路径部分。

当主机名中出现非 ASCII 字符时，主机名将使用 [Punycode] 算法进行编码。
但是，主机名可能同时包含 Punycode 编码和百分比编码的字符：

```js
const myURL = new URL('https://%CF%80.example.com/foo');
console.log(myURL.href);
// 打印 https://xn--1xa.example.com/foo
console.log(myURL.origin);
// 打印 https://xn--1xa.example.com
```

