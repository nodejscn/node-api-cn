
* Returns {AsyncHook} A reference to `asyncHook`.

Disable the callbacks for a given `AsyncHook` instance from the global pool of
AsyncHook callbacks to be executed. Once a hook has been disabled it will not
be called again until enabled.

For API consistency `disable()` also returns the `AsyncHook` instance.

