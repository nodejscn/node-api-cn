
* Returns: {net.Socket} The socket itself.

Pauses the reading of data. That is, [`'data'`][] events will not be emitted.
Useful to throttle back an upload.

