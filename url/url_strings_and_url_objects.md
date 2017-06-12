
一个 URL 字符串是一个结构化的字符串，它包含多个有意义的组成部分。
当被解析时，会返回一个 URL 对象，它包含每个组成部分作为属性。

The `url` module provides two APIs for working with URLs: a legacy API that is
Node.js specific, and a newer API that implements the same
[WHATWG URL Standard][] used by web browsers.

*Note*: While the Legacy API has not been deprecated, it is maintained solely
for backwards compatibility with existing applications. New application code
should use the WHATWG API.

A comparison between the WHATWG and Legacy APIs is provided below. Above the URL
`'http://user:pass@sub.host.com:8080/p/a/t/h?query=string#hash'`, properties of
an object returned by the legacy `url.parse()` are shown. Below it are
properties of a WHATWG `URL` object.

*Note*: WHATWG URL's `origin` property includes `protocol` and `host`, but not
`username` or `password`.

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

Parsing the URL string using the WHATWG API:

```js
const { URL } = require('url');
const myURL =
  new URL('https://user:pass@sub.host.com:8080/p/a/t/h?query=string#hash');
```

*Note*: In Web Browsers, the WHATWG `URL` class is a global that is always
available. In Node.js, however, the `URL` class must be accessed via
`require('url').URL`.

Parsing the URL string using the Legacy API:

```js
const url = require('url');
const myURL =
  url.parse('https://user:pass@sub.host.com:8080/p/a/t/h?query=string#hash');
```

