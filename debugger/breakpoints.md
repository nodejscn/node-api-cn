
* `setBreakpoint()`, `sb()` - 在当前行设置断点
* `setBreakpoint(line)`, `sb(line)` - 在指定行设置断点
* `setBreakpoint('fn()')`, `sb(...)` - 在函数体的第一条语句设置断点
* `setBreakpoint('script.js', 1)`, `sb(...)` - 在 script.js 的第 1 行设置断点
* `clearBreakpoint('script.js', 1)`, `cb(...)` - 清除 script.js 第 1 行的断点

也可以在一个还未被加载的文件（模块）中设置断点：

```txt
$ node debug test/fixtures/break-in-module/main.js
< debugger listening on port 5858
connecting to port 5858... ok
break in test/fixtures/break-in-module/main.js:1
  1 var mod = require('./mod.js');
  2 mod.hello();
  3 mod.hello();
debug> setBreakpoint('mod.js', 23)
Warning: script 'mod.js' was not loaded yet.
  1 var mod = require('./mod.js');
  2 mod.hello();
  3 mod.hello();
debug> c
break in test/fixtures/break-in-module/mod.js:23
 21
 22 exports.hello = () => {
 23   return 'hello from module';
 24 };
 25
debug>
```

