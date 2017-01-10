<!-- YAML
added: v0.9.3
-->

* {String}

Provides the platform-specific path delimiter:

* `;` for Windows
* `:` for POSIX

For example, on POSIX:

```js
console.log(process.env.PATH)
// Prints: '/usr/bin:/bin:/usr/sbin:/sbin:/usr/local/bin'

process.env.PATH.split(path.delimiter)
// Returns: ['/usr/bin', '/bin', '/usr/sbin', '/sbin', '/usr/local/bin']
```

On Windows:

```js
console.log(process.env.PATH)
// Prints: 'C:\Windows\system32;C:\Windows;C:\Program Files\node\'

process.env.PATH.split(path.delimiter)
// Returns: ['C:\\Windows\\system32', 'C:\\Windows', 'C:\\Program Files\\node\\']
```

