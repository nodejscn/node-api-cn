
[`child_process.spawnSync()`]、[`child_process.execSync()`] 和 [`child_process.execFileSync()`] 方法是**同步的**且**会**阻塞 Node.js 的事件循环，暂停任何额外代码的执行直到衍生的进程退出。

像这样的阻塞调用有利于简化普通用途的脚本任务，且启动时有利于简化应用配置的加载/处理。

