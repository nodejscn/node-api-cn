
When calling [`Buffer.allocUnsafe()`] and [`Buffer.allocUnsafeSlow()`], the
segment of allocated memory is *uninitialized* (it is not zeroed-out). While
this design makes the allocation of memory quite fast, the allocated segment of
memory might contain old data that is potentially sensitive. Using a `Buffer`
created by [`Buffer.allocUnsafe()`] without *completely* overwriting the memory
can allow this old data to be leaked when the `Buffer` memory is read.

While there are clear performance advantages to using [`Buffer.allocUnsafe()`],
extra care *must* be taken in order to avoid introducing security
vulnerabilities into an application.

