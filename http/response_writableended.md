<!-- YAML
added: v12.9.0
-->

* {boolean}

Is `true` after [`response.end()`][] has been called. This property
does not indicate whether the data has been flushed, for this use
[`response.writableFinished`][] instead.

