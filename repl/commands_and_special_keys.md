
所有 REPL 的实例都支持下列特殊命令：

* `.break` - 在输入多行表达式的过程中，输入`.break` 命令（或按下 `<ctrl>-C` 组合键）将终止表达式的继续输入。
* `.clear` - 复位 REPL `context`，使之成为空的对象并清除所有当前输入的多行表达式。
* `.exit` - 关闭输入输出界面，导致 REPL 退出。
* `.help` - 显示特定命令的帮助列表。
* `.save` - 保存当前 REPL 会话到一个文件：
  `> .save ./file/to/save.js`
* `.load` - 读取一个文件到当前 REPL 会话。
  `> .load ./file/to/load.js`
* `.editor` 进入编辑模式（`<ctrl>-D` 完成，`<ctrl>-C` 取消）

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

REPL 中下列按键组合有特殊效果：

* `<ctrl>-C` - 按下一次，与 `.break` 命令的效果一致。在空白行上按下两次，与 `.exit` 命令的效果一致。
* `<ctrl>-D` - 与 `.exit` 命令的效果一致。
* `<tab>` - 在空白行，显示全局和本地范围内的变量。在输入命令时按下，显示相似的自动补完选项。

