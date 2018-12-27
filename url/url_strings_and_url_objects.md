
URL 字符串是结构化的字符串，包含多个含义不同的组成部分。
解析字符串后返回的 URL 对象，每个属性对应字符串的各个组成部分。

`url` 模块提供了两套 API 来处理 URL：一个是旧版本遗留的 API，一个是实现了 [WHATWG标准][WHATWG URL Standard]的新 API。

遗留的 API 还没有被废弃，保留是为了兼容已存在的应用程序。
新的应用程序应使用 WHATWG 的 API。

WHATWG 的 API 与遗留的 API 的区别如下。
在下图中，URL `'http://user:pass@sub.example.com:8080/p/a/t/h?query=string#hash'` 上方的是遗留的 `url.parse()` 返回的对象的属性。
下方的则是 WHATWG 的 `URL` 对象的属性。

WHATWG 的 `origin` 属性包括 `protocol` 和 `host`，但不包括 `username` 或 `password`。

```txt
┌────────────────────────────────────────────────────────────────────────────────────────────────┐
│                                              href                                              │
├──────────┬──┬─────────────────────┬────────────────────────┬───────────────────────────┬───────┤
│ protocol │  │        auth         │          host          │           path            │ hash  │
│          │  │                     ├─────────────────┬──────┼──────────┬────────────────┤       │
│          │  │                     │    hostname     │ port │ pathname │     search     │       │
│          │  │                     │                 │      │          ├─┬──────────────┤       │
│          │  │                     │                 │      │          │ │    query     │       │
"  https:   //    user   :   pass   @ sub.example.com : 8080   /p/a/t/h  ?  query=string   #hash "
│          │  │          │          │    hostname     │ port │          │                │       │
│          │  │          │          ├─────────────────┴──────┤          │                │       │
│ protocol │  │ username │ password │          host          │          │                │       │
├──────────┴──┼──────────┴──────────┼────────────────────────┤          │                │       │
│   origin    │                     │         origin         │ pathname │     search     │ hash  │
├─────────────┴─────────────────────┴────────────────────────┴──────────┴────────────────┴───────┤
│                                              href                                              │
└────────────────────────────────────────────────────────────────────────────────────────────────┘
```

使用 WHATWG 的 API 解析 URL 字符串：

```js
const myURL =
  new URL('https://user:pass@sub.host.com:8080/p/a/t/h?query=string#hash');
```

使用遗留的 API 解析 URL 字符串：
```js
const url = require('url');
const myURL =
  url.parse('https://user:pass@sub.host.com:8080/p/a/t/h?query=string#hash');
```

