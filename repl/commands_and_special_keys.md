
The following special commands are supported by all REPL instances:
所有REPL的实例都支持下列特殊命令：

* `.break` - When in the process of inputting a multi-line expression, entering
  the `.break` command (or pressing the `<ctrl>-C` key combination) will abort
  further input or processing of that expression.
* `.break` - 在输入多行表达式的过程中，输入`.break`命令（或按下`<ctrl>-C`组合键）将终止表达式的继续输入。

* `.clear` - Resets the REPL `context` to an empty object and clears any
  multi-line expression currently being input.
* `.clear` - 复位REPL `context` ，使之成为空的对象并清除所有当前输入的多行表达式。

* `.exit` - Close the I/O stream, causing the REPL to exit.
* `.exit` - 关闭输入输出界面，导致REPL退出。

* `.help` - Show this list of special commands.
* `.help` - 显示特定命令的帮助列表

* `.save` - Save the current REPL session to a file:
* `.save` - 保存当前REPL会话到一个文件：
  `> .save ./file/to/save.js`

* `.load` - Load a file into the current REPL session.
* `.load` - 读取一个文件到当前REPL会话。
  `> .load ./file/to/load.js`

* `.editor` - Enter editor mode (`<ctrl>-D` to finish, `<ctrl>-C` to cancel)
* `.editor` 进入编辑模式（`<ctrl>-D`完成，`<ctrl>-C`取消）

```js
> .editor
// Entering editor mode (^D to finish, ^C to cancel)
function welcome(name) {
  return `Hello ${name}!`;
}

welcome('Node.js User');

// ^D
'Hello Node.js User!'
>
```

The following key combinations in the REPL have these special effects:
REPL中下列按键组合有特殊效果：

* `<ctrl>-C` - When pressed once, has the same effect as the `.break` command.
  When pressed twice on a blank line, has the same effect as the `.exit`
  command.
* `<ctrl>-C` - 按下一次，与`.break`命令的效果一致。在空白行上按下两次，与`.exit`命令的效果一致。

* `<ctrl>-D` - Has the same effect as the `.exit` command.
* `<ctrl>-D` - 与`.exit`命令的效果一致。

* `<tab>` - When pressed on a blank line, displays global and local(scope)
  variables. When pressed while entering other input, displays relevant
  autocompletion options.
* `<tab>` - 在空白行，显示全局和本地范围内的变量。在输入命令时按下，显示相似的自动补完选项。
