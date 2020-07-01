
In most cases your application or library code should have no issues with
`AsyncLocalStorage`. But in rare cases you may face situations when the
current store is lost in one of asynchronous operations. Then you should
consider the following options.

If your code is callback-based, it is enough to promisify it with
[`util.promisify()`][], so it starts working with native promises.

If you need to keep using callback-based API, or your code assumes
a custom thenable implementation, you should use [`AsyncResource`][] class
to associate the asynchronous operation with the correct execution context.














