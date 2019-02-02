
* `setBreakpoint()`, `sb()` - 在当前行上设置断点。
* `setBreakpoint(line)`, `sb(line)` - 在特定行上设置断点。
* `setBreakpoint('fn()')`, `sb(...)` - 在函数体的第一个语句上设置断点。
* `setBreakpoint('script.js', 1)`, `sb(...)` - 在 `script.js` 的第一行设置断点。
* `clearBreakpoint('script.js', 1)`, `cb(...)` - 清除 `script.js` 中第一行的断点。

也可以在尚未加载的文件（模块）中设置断点：

```txt
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
 20 // USE OR OTHER DEALINGS IN THE SOFTWARE.
 21
>22 exports.hello = function() {
 23   return 'hello from module';
 24 };
debug>
```

