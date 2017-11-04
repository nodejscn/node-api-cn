
`resource` is an object that represents the actual async resource that has
been initialized. This can contain useful information that can vary based on
the value of `type`. For instance, for the `GETADDRINFOREQWRAP` resource type,
`resource` provides the hostname used when looking up the IP address for the
hostname in `net.Server.listen()`. The API for accessing this information is
currently not considered public, but using the Embedder API, users can provide
and document their own resource objects. For example, such a resource object
could contain the SQL query being executed.

In the case of Promises, the `resource` object will have `promise` property
that refers to the Promise that is being initialized, and a `parentId` property
set to the `asyncId` of a parent Promise, if there is one, and `undefined`
otherwise. For example, in the case of `b = a.then(handler)`, `a` is considered
a parent Promise of `b`.

*Note*: In some cases the resource object is reused for performance reasons,
it is thus not safe to use it as a key in a `WeakMap` or add properties to it.

