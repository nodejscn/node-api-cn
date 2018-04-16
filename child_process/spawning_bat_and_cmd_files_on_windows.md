
[`child_process.exec()`] 和 [`child_process.execFile()`] 之间的区别会因平台而不同。
在类 Unix 操作系统（Unix、 Linux、 macOS）上，[`child_process.execFile()`] 效率更高，因为它不需要衍生 shell。
但在 Windows 上，`.bat` 和 `.cmd` 文件在没有终端的情况下是不可执行的，因此不能使用 [`child_process.execFile()`] 启动。
可以使用设置了 `shell` 选项的 [`child_process.spawn()`]、或使用 [`child_process.exec()`]、或衍生 `cmd.exe` 并将 `.bat` 或 `.cmd` 文件作为参数传入（也就是 `shell` 选项和 [`child_process.exec()`] 所做的工作）。
如果脚本文件名包含空格，则需要加上引号。

```js
// 仅限 Windows 系统
const { spawn } = require('child_process');
const bat = spawn('cmd.exe', ['/c', 'my.bat']);

bat.stdout.on('data', (data) => {
  console.log(data.toString());
});

bat.stderr.on('data', (data) => {
  console.log(data.toString());
});

bat.on('exit', (code) => {
  console.log(`子进程退出码：${code}`);
});
```

```js
// 或
const { exec } = require('child_process');
exec('my.bat', (err, stdout, stderr) => {
  if (err) {
    console.error(err);
    return;
  }
  console.log(stdout);
});

// 文件名带有空格的脚本：
const bat = spawn('"my script.cmd"', ['a', 'b'], { shell: true });
// 或：
exec('"my script.cmd" a b', (err, stdout, stderr) => {
  // ...
});
```

