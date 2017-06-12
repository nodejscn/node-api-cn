
`resource` is an object that represents the actual resource. This can contain
useful information such as the hostname for the `GETADDRINFOREQWRAP` resource
type, which will be used when looking up the ip for the hostname in
`net.Server.listen`. The API for getting this information is currently not
considered public, but using the Embedder API users can provide and document
their own resource objects. Such as resource object could for example contain
the SQL query being executed.

*Note:* In some cases the resource object is reused for performance reasons,
it is thus not safe to use it as a key in a `WeakMap` or add properties to it.

