<!--
added: v0.11.14
-->

* Returns: {Boolean}

The `readable.isPaused()` method returns the current operating state of the
Readable. This is used primarily by the mechanism that underlies the
`readable.pipe()` method. In most typical cases, there will be no reason to
use this method directly.

```js
const readable = new stream.Readable

readable.isPaused() // === false
readable.pause()
readable.isPaused() // === true
readable.resume()
readable.isPaused() // === false
```

