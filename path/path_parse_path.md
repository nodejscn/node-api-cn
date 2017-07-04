<!-- YAML
added: v0.11.15
-->

* `path` {string}
* 返回: {Object}

`path.parse()` 方法返回一个对象，对象的属性表示 `path` 的元素。
Trailing directory separators are ignored, see [`path.sep`][].

返回的对象有以下属性：

* `dir` {string}
* `root` {string}
* `base` {string}
* `name` {string}
* `ext` {string}

例如，在 POSIX 上：

```js
path.parse('/home/user/dir/file.txt');
// 返回:
// { root: '/',
//   dir: '/home/user/dir',
//   base: 'file.txt',
//   ext: '.txt',
//   name: 'file' }
```

```text
┌─────────────────────┬────────────┐
│          dir        │    base    │
├──────┬              ├──────┬─────┤
│ root │              │ name │ ext │
"  /    home/user/dir / file  .txt "
└──────┴──────────────┴──────┴─────┘
(请无视以上字符串中的空格，它们只是为了布局)
```

在 Windows 上：

```js
path.parse('C:\\path\\dir\\file.txt');
// 返回:
// { root: 'C:\\',
//   dir: 'C:\\path\\dir',
//   base: 'file.txt',
//   ext: '.txt',
//   name: 'file' }
```

```text
┌─────────────────────┬────────────┐
│          dir        │    base    │
├──────┬              ├──────┬─────┤
│ root │              │ name │ ext │
" C:\      path\dir   \ file  .txt "
└──────┴──────────────┴──────┴─────┘
(请无视以上字符串中的空格，它们只是为了布局)
```

如果 `path` 不是一个字符串，则抛出 [`TypeError`]。

