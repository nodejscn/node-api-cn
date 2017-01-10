
The Readable stream API evolved across multiple Node.js versions and provides
multiple methods of consuming stream data. In general, developers should choose
*one* of the methods of consuming data and *should never* use multiple methods
to consume data from a single stream.

Use of the `readable.pipe()` method is recommended for most users as it has been
implemented to provide the easiest way of consuming stream data. Developers that
require more fine-grained control over the transfer and generation of data can
use the [`EventEmitter`][] and `readable.pause()`/`readable.resume()` APIs.

