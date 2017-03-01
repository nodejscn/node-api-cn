<!-- YAML
added: v0.3.4
-->

The `rl.pause()` method pauses the `input` stream, allowing it to be resumed
later if necessary.

`rl.pause()`函数中止输入流，如果稍后还需要的话，它允许被唤醒。

Calling `rl.pause()` does not immediately pause other events (including
`'line'`) from being emitted by the `readline.Interface` instance.

调用`rl.pause()`不会立刻中止`readline.Interface`实例创建的其它事件（包括`'line'`）。
