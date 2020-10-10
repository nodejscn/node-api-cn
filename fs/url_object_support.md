<!-- YAML
added: v7.6.0
-->

对于大多数 `fs` 模块的函数，`path` 或 `filename` 参数可以传入 WHATWG [`URL`] 对象。
仅支持使用 `file:` 协议的 [`URL`] 对象。

```js
const fs = require('fs');
const fileUrl = new URL('file:///文件');

fs.readFileSync(fileUrl);
```

`file:` URL 始终是绝对路径。

使用 WHATWG [`URL`] 对象可能会采用特定于平台的行为。

在 Windows 上，带有主机名的 `file:` URL 会转换为 UNC 路径，而带有驱动器号的 `file:` URL 会转换为本地的绝对路径。
没有主机名和驱动器号的 `file:` URL 会导致抛出错误：

```js
// 在 Windows 上：

// - 带有主机名的 WHATWG 文件的 URL 会转换为 UNC 路径。
// file://主机名/文件 => \\主机名\文件
fs.readFileSync(new URL('file://主机名/文件'));

// - 带有驱动器号的 WHATWG 文件的 URL 会转换为绝对路径。
// file:///C:/文件 => C:\文件
fs.readFileSync(new URL('file:///C:/文件'));

// - 没有主机名的 WHATWG 文件的 URL 必须包含驱动器号。
fs.readFileSync(new URL('file:///无驱动器号/文件'));
fs.readFileSync(new URL('file:///文件'));
// TypeError [ERR_INVALID_FILE_URL_PATH]: File URL path must be absolute
```

带有驱动器号的 `file:` URL 必须使用 `:` 作为驱动器号后面的分隔符。
使用其他分隔符会导致抛出错误。

在所有其他平台上，不支持带有主机名的 `file:` URL，使用时会导致抛出错误：

```js
// 在其他平台上：

// - 不支持带有主机名的 WHATWG 文件的 URL。
// file://主机名/文件 => 抛出错误!
fs.readFileSync(new URL('file://主机名/文件'));
// TypeError [ERR_INVALID_FILE_URL_PATH]: must be absolute

// - WHATWG 文件的 URL 会转换为绝对路径。
// file:///文件 => /文件
fs.readFileSync(new URL('file:///文件'));
```

包含编码后的斜杆字符的 `file:` URL 在所有平台上都会导致抛出错误：

```js
// 在 Windows 上：
fs.readFileSync(new URL('file:///C:/%2F'));
fs.readFileSync(new URL('file:///C:/%2f'));
/* TypeError [ERR_INVALID_FILE_URL_PATH]: File URL path must not include encoded
\ or / characters */

// 在 POSIX 上：
fs.readFileSync(new URL('file:///%2F'));
fs.readFileSync(new URL('file:///%2f'));
/* TypeError [ERR_INVALID_FILE_URL_PATH]: File URL path must not include encoded
/ characters */
```

在 Windows 上，包含编码后的反斜杆字符的 `file:` URL 会导致抛出错误： 

```js
// 在 Windows 上：
fs.readFileSync(new URL('file:///C:/%5C'));
fs.readFileSync(new URL('file:///C:/%5c'));
/* TypeError [ERR_INVALID_FILE_URL_PATH]: File URL path must not include encoded
\ or / characters */
```

