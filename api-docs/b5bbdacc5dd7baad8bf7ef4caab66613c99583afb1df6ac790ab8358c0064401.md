<!-- YAML
added: v5.10.0
-->

Set V8's thread pool size which will be used to allocate background jobs.

If set to `0` then V8 will choose an appropriate size of the thread pool based
on the number of online processors.

If the value provided is larger than V8's maximum, then the largest value
will be chosen.

