
`resource` is an object that represents the actual async resource that has
been initialized. This can contain useful information that can vary based on
the value of `type`. For instance, for the `GETADDRINFOREQWRAP` resource type,
`resource` provides the host name used when looking up the IP address for the
host in `net.Server.listen()`. The API for accessing this information is
currently not considered public, but using the Embedder API, users can provide
and document their own resource objects. For example, such a resource object
could contain the SQL query being executed.

In the case of Promises, the `resource` object will have an
`isChainedPromise` property, set to `true` if the promise has a parent promise,
and `false` otherwise. For example, in the case of `b = a.then(handler)`, `a` is
considered a parent `Promise` of `b`. Here, `b` is considered a chained promise.

In some cases the resource object is reused for performance reasons, it is
thus not safe to use it as a key in a `WeakMap` or add properties to it.

