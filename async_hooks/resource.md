
`resource` is an object that represents the actual resource. This can contain
useful information such as the hostname for the `GETADDRINFOREQWRAP` resource
type, which will be used when looking up the ip for the hostname in
`net.Server.listen`. The API for getting this information is currently not
considered public, but using the Embedder API users can provide and document
their own resource objects. Such as resource object could for example contain
the SQL query being executed.

In the case of Promises, the `resource` object will have `promise` property
that refers to the Promise that is being initialized, and a `parentId` property
that equals the `asyncId` of a parent Promise, if there is one, and
`undefined` otherwise. For example, in the case of `b = a.then(handler)`,
`a` is considered a parent Promise of `b`.

*Note*: In some cases the resource object is reused for performance reasons,
it is thus not safe to use it as a key in a `WeakMap` or add properties to it.

