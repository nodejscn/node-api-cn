
可读流事实上工作在下面两种模式之一：flowing 和 paused 。

在 flowing 模式下， 可读流自动从系统底层读取数据，并通过 [`EventEmitter`][] 接口的事件尽快将数据提供给应用。

在 paused 模式下，必须显式调用 [`stream.read()`][stream-read] 方法来从流中读取数据片段。

所有初始工作模式为 paused 的 [Readable][] 流，可以通过下面三种途径切换到 flowing
模式：

* 监听 [`'data'`][] 事件。
* 调用 [`stream.resume()`][stream-resume] 方法。
* 调用 [`stream.pipe()`][] 方法将数据发送到 [Writable][]。

可读流可以通过下面途径切换到 paused 模式：

* 如果不存在管道目标（pipe destination），可以通过调用
  [`stream.pause()`][stream-pause] 方法实现。
* 如果存在管道目标，可以通过取消 [`'data'`][] 事件监听，并调用 [`stream.unpipe()`][] 方法移除所有管道目标来实现。

这里需要记住的重要概念就是，可读流需要先为其提供消费或忽略数据的机制，才能开始提供数据。如果消费机制被禁用或取消，可读流将 *尝试*
停止生成数据。

*注意*: 为了向后兼容，取消 [`'data'`][] 事件监听并 **不会** 自动将流暂停。同时，如果存在管道目标（pipe destination），且目标状态变为可以接收数据（drain and ask for
more data），调用了 [`stream.pause()`][stream-pause] 方法也并不保证流会一直 *保持* 暂停状态。

*注意*: 如果 [Readable][] 切换到 flowing 模式，且没有消费者处理流中的数据，这些数据将会丢失。
比如， 调用了 `readable.resume()` 方法却没有监听 `'data'` 事件，或是取消了 `'data'` 事件监听，就有可能出现这种情况。

