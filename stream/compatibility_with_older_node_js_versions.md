
<!--type=misc-->

在v0.10之前的Node.js版本中，可读流接口更简单，但功能更弱，功能更少。

* 相比需要等待[`stream.read()`][stream-read] 方法调用之后才触发，[`'data'`][] 事件自己会立即触发。 需要执行一定量工作来决定如何处理数据的应用程序需要将读取数据存储到缓冲区中，以便数据不会丢失。
* The [`stream.pause()`][stream-pause] 方法是建议性的，而不是保证。 这意味着即使流处于暂停状态，仍然需要准备接收`data`事件。

在Node.js v0.10中，添加了[Readable][]类。 为了向后兼容较旧的Node.js程序，当添加`data`事件处理程序或调用[`stream.resume()`][stream-resume]方法时，可读流将切换到“流动模式”。 结果是，即使不使用新的[`stream.read()`][stream-read]方法和[`'readable'`][]事件，也不必担心丢失[`'data'`][]块。

虽然大多数应用程序将继续正常工作，但在以下情况下会引入极端情况：

* 未添加[`'data'`][] 事件监听。
* 未调用[`stream.resume()`][stream-resume]方法。
* 通过管道没有传送到任何可写的目的地。

例如，请考虑以下代码：

```js
// WARNING!  BROKEN!
net.createServer((socket) => {

  // we add an 'end' method, but never consume the data
  socket.on('end', () => {
    // It will never get here.
    socket.end('The message was received but was not processed.\n');
  });

}).listen(1337);
```

在v0.10之前的Node.js版本中，传入的消息数据将会是简单地丢弃。 但是，在Node.js v0.10及更高版本中，套接字仍然存在永远停顿。

在这种情况下的解决方法是调用[`stream.resume()`][stream-resume] 开始读取数据：

```js
// Workaround
net.createServer((socket) => {

  socket.on('end', () => {
    socket.end('The message was received but was not processed.\n');
  });

  // start the flow of data, discarding it.
  socket.resume();

}).listen(1337);
```

除了新的可读流切换到流动模式之外，pre-v0.10风格的流可以使用包装在Readable类中[`readable.wrap()`][`stream.wrap()`] 方法。


