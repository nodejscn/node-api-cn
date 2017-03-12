<!-- YAML
added: v0.1.91
-->

* `选项` {Object}
  * `prompt` {String} 输入行显示的提示符。默认为`> `。
  * `input` {Readable} 可读的输入流，REPL的输入可以从哪里读取。默认是`process.stdin`。
  * `output` {Writable} 可写的输出流，REPL的输出可以写到哪里。默认是`process.stdout`。
  * `terminal` {boolean} 如果是`true`，规定`output`必须当作TTY终端来处理，并且可以使用
    ANSI/VT100转意编码写入。默认在初始化时，跟随`output`的`isTTY`属性的值。
  * `eval` {Function} 当每个输入的行被解释时调用该函数。默认是JavaScript `eval()`函数的异
    步封装。`eval`函数可以使用`repl.Recoverable`抛出异常，用以提示不完整输入以及提示附加信息。
  * `useColors` {boolean} 如果是`true`，规定默认的`writer`函数必须在REPL输出中包含ANSI颜色风
    格。如果使用用户定义的`writer`函数，那么该参数无效。默认使用REPL实例的`terminal`属性的值。
  * `useGlobal` {boolean} 如果是`true`，规定默认的解释函数使用JavaScript `global`，作为上下文
    （context）而不是为REPL实例创建一个新的独立的上下文。默认是`false`。
  * `ignoreUndefined` {boolean} 如果是`true`，规定默认的writer不再输出命令返回的`undefined`值。
     默认是`false`。
  * `writer` {Function} 在写出至`output`之前，该函数被调用用来格式化每个命令的输出。默认是
    [`util.inspect()`][].
  * `completer` {Function} 是一个可选函数，用来自定义Tab键自动完成功能。参见实例[`readline.InterfaceCompleter`][]。
  * `replMode` - 一个标志位，用来指定默认的解释器用何种方式执行JavaScript命令。可选strict模式，
    默认模式或综合模式("魔术"模式)。可以接受的值有：
    * `repl.REPL_MODE_SLOPPY` - 使用sloppy模式解释表达式。
    * `repl.REPL_MODE_STRICT` - 使用strict模式解释表达式。该模式等同于在每个repl声明前加上`'use strict'`。
    * `repl.REPL_MODE_MAGIC` - 尝试使用默认模式解释表达式。如果表达式解释出错，再使用strict模式重试。
  * `breakEvalOnSigint` - 收到`SIGINT`后，停止解释当前代码。比如，按下`Ctrl+C`。不能和自定义的`eval`函数
     共同使用。默认值是`false`。

`repl.start()`函数创建并启动一个`repl.REPLServer`实例。

