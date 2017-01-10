
The [`'finish'`][] and [`'end'`][] events are from the `stream.Writable`
and `stream.Readable` classes, respectively. The `'finish'` event is emitted
after [`stream.end()`][stream-end] is called and all chunks have been processed
by [`stream._transform()`][stream-_transform]. The `'end'` event is emitted
after all data has been output, which occurs after the callback in
[`transform._flush()`][stream-_flush] has been called.

