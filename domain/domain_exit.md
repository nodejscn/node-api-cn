
The `exit` method exits the current domain, popping it off the domain stack.
Any time execution is going to switch to the context of a different chain of
asynchronous calls, it's important to ensure that the current domain is exited.
The call to `exit` delimits either the end of or an interruption to the chain
of asynchronous calls and I/O operations bound to a domain.

If there are multiple, nested domains bound to the current execution context,
`exit` will exit any domains nested within this domain.

Calling `exit` changes only the active domain, and does not alter the domain
itself. `enter` and `exit` can be called an arbitrary number of times on a
single domain.

If the domain on which `exit` is called has been disposed, `exit` will return
without exiting the domain.

