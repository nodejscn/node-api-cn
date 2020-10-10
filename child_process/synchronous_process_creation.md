
[`child_process.spawnSync()`]、[`child_process.execSync()`] 和 [`child_process.execFileSync()`] 方法是同步的，并且将会阻塞 Node.js 事件循环、暂停任何其他代码的执行，直到衍生的进程退出。

阻塞这些调用对于简化通用的脚本任务和简化应用程序配置在启动时的加载或处理都非常有用。

