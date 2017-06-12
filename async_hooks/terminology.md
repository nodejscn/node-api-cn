
An asynchronous resource represents an object with an associated callback.
This callback may be called multiple times, for example, the `connection` event
in `net.createServer`, or just a single time like in `fs.open`. A resource
can also be closed before the callback is called. AsyncHook does not
explicitly distinguish between these different cases but will represent them
as the abstract concept that is a resource.

