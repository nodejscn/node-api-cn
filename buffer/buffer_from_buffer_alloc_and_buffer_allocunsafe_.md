
In versions of Node.js prior to v6, `Buffer` instances were created using the
`Buffer` constructor function, which allocates the returned `Buffer`
differently based on what arguments are provided:

* Passing a number as the first argument to `Buffer()` (e.g. `new Buffer(10)`),
  allocates a new `Buffer` object of the specified size. The memory allocated
  for such `Buffer` instances is *not* initialized and *can contain sensitive
  data*. Such `Buffer` instances *must* be initialized *manually* by using either
  [`buf.fill(0)`][`buf.fill()`] or by writing to the `Buffer` completely. While
  this behavior is *intentional* to improve performance, development experience
  has demonstrated that a more explicit distinction is required between creating
  a fast-but-uninitialized `Buffer` versus creating a slower-but-safer `Buffer`.
* Passing a string, array, or `Buffer` as the first argument copies the
  passed object's data into the `Buffer`.
* Passing an [`ArrayBuffer`] returns a `Buffer` that shares allocated memory with
  the given [`ArrayBuffer`].

Because the behavior of `new Buffer()` changes significantly based on the type
of value passed as the first argument, applications that do not properly
validate the input arguments passed to `new Buffer()`, or that fail to
appropriately initialize newly allocated `Buffer` content, can inadvertently
introduce security and reliability issues into their code.

To make the creation of `Buffer` instances more reliable and less error prone,
the various forms of the `new Buffer()` constructor have been **deprecated**
and replaced by separate `Buffer.from()`, [`Buffer.alloc()`], and
[`Buffer.allocUnsafe()`] methods.

*Developers should migrate all existing uses of the `new Buffer()` constructors
to one of these new APIs.*

* [`Buffer.from(array)`] returns a new `Buffer` containing a *copy* of the provided
  octets.
* [`Buffer.from(arrayBuffer[, byteOffset [, length]])`][`Buffer.from(arrayBuffer)`]
  returns a new `Buffer` that *shares* the same allocated memory as the given
  [`ArrayBuffer`].
* [`Buffer.from(buffer)`] returns a new `Buffer` containing a *copy* of the
  contents of the given `Buffer`.
* [`Buffer.from(string[, encoding])`][`Buffer.from(string)`] returns a new `Buffer`
  containing a *copy* of the provided string.
* [`Buffer.alloc(size[, fill[, encoding]])`][`Buffer.alloc()`] returns a "filled"
  `Buffer` instance of the specified size. This method can be significantly
  slower than [`Buffer.allocUnsafe(size)`][`Buffer.allocUnsafe()`] but ensures
  that newly created `Buffer` instances never contain old and potentially
  sensitive data.
* [`Buffer.allocUnsafe(size)`][`Buffer.allocUnsafe()`] and
  [`Buffer.allocUnsafeSlow(size)`][`Buffer.allocUnsafeSlow()`] each return a
  new `Buffer` of the specified `size` whose content *must* be initialized
  using either [`buf.fill(0)`][`buf.fill()`] or written to completely.

`Buffer` instances returned by [`Buffer.allocUnsafe()`] *may* be allocated off
a shared internal memory pool if `size` is less than or equal to half
[`Buffer.poolSize`]. Instances returned by [`Buffer.allocUnsafeSlow()`] *never*
use the shared internal memory pool.

