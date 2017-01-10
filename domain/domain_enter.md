
The `enter` method is plumbing used by the `run`, `bind`, and `intercept`
methods to set the active domain. It sets `domain.active` and `process.domain`
to the domain, and implicitly pushes the domain onto the domain stack managed
by the domain module (see [`domain.exit()`][] for details on the domain stack). The
call to `enter` delimits the beginning of a chain of asynchronous calls and I/O
operations bound to a domain.

Calling `enter` changes only the active domain, and does not alter the domain
itself. `enter` and `exit` can be called an arbitrary number of times on a
single domain.

If the domain on which `enter` is called has been disposed, `enter` will return
without setting the domain.

