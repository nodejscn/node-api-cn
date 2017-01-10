
The default operation of the `path` module varies based on the operating system
on which a Node.js application is running. Specifically, when running on a
Windows operating system, the `path` module will assume that Windows-style
paths are being used.

For example, using the `path.basename()` function with the Windows file path
`C:\temp\myfile.html`, will yield different results when running on POSIX than
when run on Windows:

On POSIX:

```js
path.basename('C:\\temp\\myfile.html');
// Returns: 'C:\temp\myfile.html'
```

On Windows:

```js
path.basename('C:\\temp\\myfile.html');
// Returns: 'myfile.html'
```

To achieve consistent results when working with Windows file paths on any
operating system, use [`path.win32`][]:

On POSIX and Windows:

```js
path.win32.basename('C:\\temp\\myfile.html');
// Returns: 'myfile.html'
```

To achieve consistent results when working with POSIX file paths on any
operating system, use [`path.posix`][]:

On POSIX and Windows:

```js
path.posix.basename('/tmp/myfile.html');
// Returns: 'myfile.html'
```

