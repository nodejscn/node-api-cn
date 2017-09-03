
一个 URL 字符串是一个结构化的字符串，它包含多个有意义的组成部分。
当被解析时，会返回一个 URL 对象，它包含每个组成部分作为属性。

`url`模块提供了两套API来处理URLs：一个是Node.js遗留的特有的API,另一个则是通常使用在web浏览器中
实现了[WHATWG URL Standard]的API.

<!--The `url` module provides two APIs for working with URLs: a legacy API that is
Node.js specific, and a newer API that implements the same
[WHATWG URL Standard][] used by web browsers.-->

*请注意*: 虽然Node.js遗留的特有的API并没有被弃用，但是保留的目的是用于向后兼容已有应用程序。因此新的应用程序请使用WHATWG API。
<!--*Note*: While the Legacy API has not been deprecated, it is maintained solely
for backwards compatibility with existing applications. New application code
should use the WHATWG API.-->

WHATWG与Node.js遗留的特有的API的比较如下。网址`'http://user:pass@sub.host.com:8080/p/a/t/h?query=string#hash'`上方是由遗留的`url.parse()`返回的对象属性。网址下方的则是由WHATWG `URL`对象的属性。
<!--A comparison between the WHATWG and Legacy APIs is provided below. Above the URL
`'http://user:pass@sub.host.com:8080/p/a/t/h?query=string#hash'`, properties of
an object returned by the legacy `url.parse()` are shown. Below it are
properties of a WHATWG `URL` object.-->

WHATWG URL的组织属性包括`protocol`和`host`,但不包含`username`、`password`.
<!--*Note*: WHATWG URL's `origin` property includes `protocol` and `host`, but not
`username` or `password`.-->

```txt
┌─────────────────────────────────────────────────────────────────────────────────────────────┐
│                                            href                                             │
├──────────┬──┬─────────────────────┬─────────────────────┬───────────────────────────┬───────┤
│ protocol │  │        auth         │        host         │           path            │ hash  │
│          │  │                     ├──────────────┬──────┼──────────┬────────────────┤       │
│          │  │                     │   hostname   │ port │ pathname │     search     │       │
│          │  │                     │              │      │          ├─┬──────────────┤       │
│          │  │                     │              │      │          │ │    query     │       │
"  https:   //    user   :   pass   @ sub.host.com : 8080   /p/a/t/h  ?  query=string   #hash "
│          │  │          │          │   hostname   │ port │          │                │       │
│          │  │          │          ├──────────────┴──────┤          │                │       │
│ protocol │  │ username │ password │        host         │          │                │       │
├──────────┴──┼──────────┴──────────┼─────────────────────┤          │                │       │
│   origin    │                     │       origin        │ pathname │     search     │ hash  │
├─────────────┴─────────────────────┴─────────────────────┴──────────┴────────────────┴───────┤
│                                            href                                             │
└─────────────────────────────────────────────────────────────────────────────────────────────┘
(请忽略字符串中的空格，它们只是为了格式化)
```

<!--Parsing the URL string using the WHATWG API:-->
利用WHATWG API解析一个URL字符串:
```js
const { URL } = require('url');
const myURL =
  new URL('https://user:pass@sub.host.com:8080/p/a/t/h?query=string#hash');
```
在浏览器中，WHATWG `URL`在全局总是可用的，而在Node.js中，任何情况下打开
或使用一个链接都必须事先引用'url'模块：`require('url').URL`

<!--*Note*: In Web Browsers, the WHATWG `URL` class is a global that is always
 available. In Node.js, however, the `URL` class must be accessed via
require('url').URL`.-->

<!--Parsing the URL string using the Legacy API:-->
通过Node.js提供的API解析一个URL:
```js
const url = require('url');
const myURL =
  url.parse('https://user:pass@sub.host.com:8080/p/a/t/h?query=string#hash');
```

