
There are no strict guidelines for warning types (as identified by the `name`
property) emitted by Node.js. New types of warnings can be added at any time.
A few of the warning types that are most common include:

* `'DeprecationWarning'` - Indicates use of a deprecated Node.js API or feature.
  Such warnings must include a `'code'` property identifying the
  [deprecation code][].
* `'ExperimentalWarning'` - Indicates use of an experimental Node.js API or
  feature. Such features must be used with caution as they may change at any
  time and are not subject to the same strict semantic-versioning and long-term
  support policies as supported features.
* `'MaxListenersExceededWarning'` - Indicates that too many listeners for a
  given event have been registered on either an `EventEmitter` or `EventTarget`.
  This is often an indication of a memory leak.
* `'TimeoutOverflowWarning'` - Indicates that a numeric value that cannot fit
  within a 32-bit signed integer has been provided to either the `setTimeout()`
  or `setInterval()` functions.
* `'UnsupportedWarning'` - Indicates use of an unsupported option or feature
  that will be ignored rather than treated as an error. One example is use of
  the HTTP response status message when using the HTTP/2 compatibility API.

