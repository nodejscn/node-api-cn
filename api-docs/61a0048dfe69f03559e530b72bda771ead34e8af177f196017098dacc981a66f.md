<!-- YAML
added: v7.6.0
-->

对于大多数 `fs` 模块的函数，`path` 或 `filename` 参数可以传入 WHATWG [`URL`] 对象。
仅支持使用 `file:` 协议的 [`URL`] 对象。

```js
const fs = require('fs');
const fileUrl = new URL('file:///tmp/hello');

fs.readFileSync(fileUrl);
```

`file:` URL 始终是绝对路径。

使用 WHATWG [`URL`] 对象可能会采用特定于平台的行为。

在 Windows 上，带有主机名的 `file:` URL 转换为 UNC 路径，而带有驱动器号的 `file:` URL 转换为本地绝对路径。
没有主机名和驱动器号的 `file:` URL 将导致抛出错误：

```js
// 在 Windows 上：

// - 带有主机名的 WHATWG 文件的 URL 转换为 UNC 路径。
// file://hostname/p/a/t/h/file => \\hostname\p\a\t\h\file
fs.readFileSync(new URL('file://hostname/p/a/t/h/file'));

// - 带有驱动器号的 WHATWG 文件的 URL 转换为绝对路径。
// file:///C:/tmp/hello => C:\tmp\hello
fs.readFileSync(new URL('file:///C:/tmp/hello'));

// - 没有主机名的 WHATWG 文件的 URL 必须包含驱动器号。
fs.readFileSync(new URL('file:///notdriveletter/p/a/t/h/file'));
fs.readFileSync(new URL('file:///c/p/a/t/h/file'));
// TypeError [ERR_INVALID_FILE_URL_PATH]: File URL path must be absolute
```

带有驱动器号的 `file:` URL 必须使用 `:` 作为驱动器号后面的分隔符。
使用其他分隔符将导致抛出错误。

在所有其他平台上，不支持带有主机名的 `file:` URL，使用时将导致抛出错误：

```js
// 在其他平台上：

// - 不支持带有主机名的 WHATWG 文件的 URL。
// file://hostname/p/a/t/h/file => throw!
fs.readFileSync(new URL('file://hostname/p/a/t/h/file'));
// TypeError [ERR_INVALID_FILE_URL_PATH]: must be absolute

// - WHATWG 文件的 URL 转换为绝对路径。
// file:///tmp/hello => /tmp/hello
fs.readFileSync(new URL('file:///tmp/hello'));
```

包含编码后的斜杆字符（`%2F`）的 `file:` URL 在所有平台上都将导致抛出错误：

```js
// 在 Windows 上：
fs.readFileSync(new URL('file:///C:/p/a/t/h/%2F'));
fs.readFileSync(new URL('file:///C:/p/a/t/h/%2f'));
/* TypeError [ERR_INVALID_FILE_URL_PATH]: File URL path must not include encoded
\ or / characters */

// 在 POSIX 上：
fs.readFileSync(new URL('file:///p/a/t/h/%2F'));
fs.readFileSync(new URL('file:///p/a/t/h/%2f'));
/* TypeError [ERR_INVALID_FILE_URL_PATH]: File URL path must not include encoded
/ characters */
```

在 Windows 上，包含编码后的反斜杆字符（`%5C`）的 `file:` URL 将导致抛出错误： 

```js
// 在 Windows 上：
fs.readFileSync(new URL('file:///C:/path/%5C'));
fs.readFileSync(new URL('file:///C:/path/%5c'));
/* TypeError [ERR_INVALID_FILE_URL_PATH]: File URL path must not include encoded
\ or / characters */
```

