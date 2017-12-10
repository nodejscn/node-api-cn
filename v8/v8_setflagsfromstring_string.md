<!-- YAML
added: v1.0.0
-->

`v8.setFlagsFromString()`可以被用来在脚本中设置V8引擎的命令行标识。此方法应该谨慎使用。在虚拟机已经运行后修改其设置可能会造成不可预测的结果，包括崩溃和数据丢失，或者一点作用也没有。

针对一个特定版本的Node.js，可供其使用的V8选项可以通过运行`node --v8-options`来获取。一个非官方的，由社区维护的选项清单及其效果可参见[这里][here]。

用法:

```js
// Print GC events to stdout for one minute.
const v8 = require('v8');
v8.setFlagsFromString('--trace_gc');
setTimeout(function() { v8.setFlagsFromString('--notrace_gc'); }, 60e3);
```

