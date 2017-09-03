
所有 REPL 的实例都支持下列特殊命令：

* `.break` - 在输入一个多行表达式的过程中，输入 `.break` 命令（或按下 `<ctrl>-C` 组合键）将终止表达式的继续输入。
* `.clear` - 重置 REPL 的 `context` 为一个空对象，并清除当前正输入的所有多行表达式。
* `.exit` - 关闭输入输出流，退出 REPL。
* `.help` - 显示特定命令的帮助列表。
* `.save` - 保存当前 REPL 会话到一个文件：
  `> .save ./file/to/save.js`
* `.load` - 读取一个文件到当前 REPL 会话。
  `> .load ./file/to/load.js`
* `.editor` 进入编辑模式（`<ctrl>-D` 完成，`<ctrl>-C` 取消）

<!-- eslint-skip -->
```js
> .editor
// 进入编辑模式（^D 完成，^C 取消）
function welcome(name) {
  return `你好 ${name}！`;
}

welcome('Node.js 用户');

// ^D
'你好 Node.js 用户！'
>
```

REPL 中下列按键组合有特殊作用：

* `<ctrl>-C` - 当按下一次时，与 `.break` 命令的效果一样。当在空白行按下两次时，与 `.exit` 命令的效果一样。
* `<ctrl>-D` - 与 `.exit` 命令的效果一样。
* `<tab>` - 当在空白行按下时，显示全局和本地作用域内的变量。当在输入时按下，显示相关的自动补全选项。

