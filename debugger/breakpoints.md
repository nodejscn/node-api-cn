
* `setBreakpoint()`, `sb()`: 在当前行上设置断点。
* `setBreakpoint(line)`, `sb(line)`: 在指定行上设置断点。
* `setBreakpoint('fn()')`, `sb(...)`: 在函数体的第一个语句上设置断点。
* `setBreakpoint('script.js', 1)`、`sb(...)`: 在 `script.js` 的第一行上设置断点。
* `setBreakpoint('script.js', 1, 'num < 4')`、`sb(...)`: 在 `script.js` 的第一行上设置条件断点，仅当 `num < 4` 计算为 `true` 时才会中断。
* `clearBreakpoint('script.js', 1)`, `cb(...)`: 清除 `script.js` 中第一行上的断点。

也可以在尚未加载的文件（模块）中设置断点：

```console
$ node inspect main.js
< Debugger listening on ws://127.0.0.1:9229/4e3db158-9791-4274-8909-914f7facf3bd
< For help, see: https://nodejs.org/en/docs/inspector
< Debugger attached.
Break on start in main.js:1
> 1 (function (exports, require, module, __filename, __dirname) { const mod = require('./mod.js');
  2 mod.hello();
  3 mod.hello();
debug> setBreakpoint('mod.js', 22)
Warning: script 'mod.js' was not loaded yet.
debug> c
break in mod.js:22
 20 // 软件中的其他处理。
 21
>22 exports.hello = function() {
 23   return '来自模块的问候';
 24 };
debug>
```

It is also possible to set a conditional breakpoint that only breaks when a
given expression evaluates to `true`:

```console
$ node inspect main.js
< Debugger listening on ws://127.0.0.1:9229/ce24daa8-3816-44d4-b8ab-8273c8a66d35
< For help, see: https://nodejs.org/en/docs/inspector
< Debugger attached.
Break on start in main.js:7
  5 }
  6
> 7 addOne(10);
  8 addOne(-1);
  9
debug> setBreakpoint('main.js', 4, 'num < 0')
  1 'use strict';
  2
  3 function addOne(num) {
> 4   return num + 1;
  5 }
  6
  7 addOne(10);
  8 addOne(-1);
  9
debug> cont
break in main.js:4
  2
  3 function addOne(num) {
> 4   return num + 1;
  5 }
  6
debug> exec('num')
-1
debug>
```


