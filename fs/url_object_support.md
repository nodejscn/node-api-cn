<!-- YAML
added: v7.6.0
-->

对于大多数 `fs` 模块的函数，`path` 或 `filename` 参数可以传入 WHATWG [`URL`] 对象。
只支持使用 `file:` 协议的 [`URL`] 对象。

```js
const fs = require('fs');
const fileUrl = new URL('file:///tmp/hello');

fs.readFileSync(fileUrl);
```

`file:` URL 必须是绝对路径。

使用 WHATWG [`URL`] 对象在不同的平台会有特定的行为。

在 Windows 上，携带主机名的 `file:` URL 会被转换为 UNC 路径，携带驱动器号的 `file:` URL 会被转换为本地绝对路径。
既没有主机名，也没有驱动器号的 `file:` URL 在转换时会抛出错误：

```js
// 在 Windows 上：

// - 携带主机名的 WHATWG 文件 URL 会被转换为 UNC 路径。
// file://hostname/p/a/t/h/file => \\hostname\p\a\t\h\file
fs.readFileSync(new URL('file://hostname/p/a/t/h/file'));

// - 携带驱动器号的 WHATWG 文件 URL 会被转换为绝对路径。
// file:///C:/tmp/hello => C:\tmp\hello
fs.readFileSync(new URL('file:///C:/tmp/hello'));

// - 没有携带主机名的 WHATWG 文件 URL 必须包含驱动器号。
fs.readFileSync(new URL('file:///notdriveletter/p/a/t/h/file'));
fs.readFileSync(new URL('file:///c/p/a/t/h/file'));
// TypeError [ERR_INVALID_FILE_URL_PATH]: File URL path must be absolute
```

携带驱动器号的 `file:` URL 必须在驱动器号后使用 `:` 作为分隔符。
使用其他分隔符会抛出错误。

在其他所有的平台上，都不支持携带主机名的 `file:` URL，使用时会抛出错误：

```js
// 在其他平台上：

// - 不支持携带主机名的 WHATWG 文件 URL。
// file://hostname/p/a/t/h/file => throw!
fs.readFileSync(new URL('file://hostname/p/a/t/h/file'));
// TypeError [ERR_INVALID_FILE_URL_PATH]: must be absolute

// - WHATWG 文件 URL 会被转换为绝对路径。
// file:///tmp/hello => /tmp/hello
fs.readFileSync(new URL('file:///tmp/hello'));
```

包含编码后的斜杆符号的 `file:` URL 在所有平台都会抛出错误：

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

在 Windows 上，包含编码后的反斜杆符号的 `file:` URL 会抛出错误： 

```js
// 在 Windows 上：
fs.readFileSync(new URL('file:///C:/path/%5C'));
fs.readFileSync(new URL('file:///C:/path/%5c'));
/* TypeError [ERR_INVALID_FILE_URL_PATH]: File URL path must not include encoded
\ or / characters */
```

