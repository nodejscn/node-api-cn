
[`child_process.exec()`] 和 [`child_process.execFile()`] 之间的重大区别会根据平台的不同而不同。
在类 Unix 操作系统上（Unix、 Linux、 macOS），[`child_process.execFile()`] 效率更高，因为它不需要衍生一个 shell。
但是在 Windows 上，`.bat` 和 `.cmd` 文件在没有终端的情况下是不可执行的，因此不能使用 [`child_process.execFile()`] 启动。
当在 Windows 下运行时，要调用 `.bat` 和 `.cmd` 文件，可以通过使用设置了 `shell` 选项的 [`child_process.spawn()`]、或使用 [`child_process.exec()`]、或衍生 `cmd.exe` 并将 `.bat` 或 `.cmd` 文件作为一个参数传入（也就是 `shell` 选项和 [`child_process.exec()`] 所做的工作）。
在任何情况下，如果脚本文件名包含了空格，则需要用加上引号。

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

