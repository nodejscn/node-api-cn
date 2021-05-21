
一个 URL 字符串是一个包含多个有意义的组件的结构化的字符串。
当被解析时，返回一个包含每个组件的属性的 URL 对象。

`url` 模块提供了两个用于处理 URL 的 API：一个 Node.js 特定的旧版的 API，一个实现了与被 Web 浏览器使用的相同的 [WHATWG URL 标准][WHATWG URL Standard]的更新的 API。

WHATWG 与旧版的 API 之间的比较提供如下。
在 URL `'https://user:pass@sub.example.com:8080/p/a/t/h?query=string#hash'` 上方展示的是旧版的 `url.parse()` 返回的一个对象的属性。
下方的则是一个 WHATWG `URL` 对象的属性。

WHATWG URL 的 `origin` 属性包括 `protocol` 和 `host`，但是不包括 `username` 或者 `password`。

```text
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
（在 "" 行中的所有空格都应该被忽略。它们纯粹是为了格式化。）
```

使用 WHATWG API 解析 URL 字符串：

```js
const myURL =
  new URL('https://user:pass@sub.example.com:8080/p/a/t/h?query=string#hash');
```

使用旧版的 API 解析 URL 字符串：

```js
const url = require('url');
const myURL =
  url.parse('https://user:pass@sub.example.com:8080/p/a/t/h?query=string#hash');
```

