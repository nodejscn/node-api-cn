<!-- YAML
added: v7.6.0
-->

对于大多数 `fs` 方法，`path` 或 `filename` 可以传入 WHATWG [`URL`]。
只支持 `file:` 协议的 [`URL`]。

```js
const fs = require('fs');
const fileUrl = new URL('file:///tmp/hello');

fs.readFileSync(fileUrl);
```

URL 必须是绝对路径。

URL 的使用因平台而异。

在 Windows 上，携带主机名的 URL 会被转换成 UNC 路径，携带驱动器号的 URL 会被转换成本地绝对路径。
主机名和驱动器号都没有的 URL 会抛出错误：

```js
// 在 Windows 上：

// - 携带主机名的 URL 会被转换成 UNC 路径。
// file://hostname/p/a/t/h/file => \\hostname\p\a\t\h\file
fs.readFileSync(new URL('file://hostname/p/a/t/h/file'));

// - 携带驱动器号的 URL 会被转换成绝对路径。
// file:///C:/tmp/hello => C:\tmp\hello
fs.readFileSync(new URL('file:///C:/tmp/hello'));

// - 主机名和驱动器号都没有的 URL 会抛出错误。
fs.readFileSync(new URL('file:///notdriveletter/p/a/t/h/file'));
fs.readFileSync(new URL('file:///c/p/a/t/h/file'));
// TypeError [ERR_INVALID_FILE_URL_PATH]: File URL path must be absolute
```

携带驱动器号的 URL 必须在驱动器号后使用 `:` 作为分隔符。
使用其他分隔符会抛出错误。

在其他平台上，都不支持携带主机名的 URL，使用时会抛出错误：

```js
// 在其他平台上：

// - 不支持携带主机名的 URL。
// file://hostname/p/a/t/h/file => throw!
fs.readFileSync(new URL('file://hostname/p/a/t/h/file'));
// TypeError [ERR_INVALID_FILE_URL_PATH]: must be absolute

// - URL 会被转换成绝对路径。
// file:///tmp/hello => /tmp/hello
fs.readFileSync(new URL('file:///tmp/hello'));
```

包含斜杆符号（`'/'`）编码的 URL 在所有平台都会抛出错误：

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

在 Windows 上，包含反斜杆符号（`'\'`）编码的 URL 也会抛出错误： 

```js
// 在 Windows 上：
fs.readFileSync(new URL('file:///C:/path/%5C'));
fs.readFileSync(new URL('file:///C:/path/%5c'));
/* TypeError [ERR_INVALID_FILE_URL_PATH]: File URL path must not include encoded
\ or / characters */
```

