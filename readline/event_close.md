<!-- YAML
added: v0.1.98
-->

The `'close'` event is emitted when one of the following occur:

* The `rl.close()` method is called and the `readline.Interface` instance has
  relinquished control over the `input` and `output` streams;
* The `input` stream receives its `'end'` event;
* The `input` stream receives `<ctrl>-D` to signal end-of-transmission (EOT);
* The `input` stream receives `<ctrl>-C` to signal `SIGINT` and there is no
  `SIGINT` event listener registered on the `readline.Interface` instance.

The listener function is called without passing any arguments.

The `readline.Interface` instance should be considered to be "finished" once
the `'close'` event is emitted.

