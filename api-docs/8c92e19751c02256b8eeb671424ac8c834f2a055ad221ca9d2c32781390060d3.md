<!-- YAML
added: v10.12.0
-->

* `url` {URL | string} 被转换为路径的文件的 URL 字符串或者 URL 对象。
* 返回: {string} 被完全解析的平台特定的 Node.js 文件路径。

此方法保证百分号编码字符解码结果的正确性，同时也确保绝对路径字符串在不同平台下的有效性。

```js
new URL('file:///C:/path/').pathname;    // 错误: /C:/path/
fileURLToPath('file:///C:/path/');       // 正确: C:\path\ (Windows)

new URL('file://nas/foo.txt').pathname;  // 错误: /foo.txt
fileURLToPath('file://nas/foo.txt');     // 正确: \\nas\foo.txt (Windows)

new URL('file:///你好.txt').pathname;    // 错误: /%E4%BD%A0%E5%A5%BD.txt
fileURLToPath('file:///你好.txt');       // 正确: /你好.txt (POSIX)

new URL('file:///hello world').pathname; // 错误: /hello%20world
fileURLToPath('file:///hello world');    // 正确: /hello world (POSIX)
```
