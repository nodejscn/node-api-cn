
Browser-compatible `URL` class, implemented by following the WHATWG URL
Standard. [Examples of parsed URLs][] may be found in the Standard itself.

*Note*: In accordance with browser conventions, all properties of `URL` objects
are implemented as getters and setters on the class prototype, rather than as
data properties on the object itself. Thus, unlike [legacy urlObject][]s, using
the `delete` keyword on any properties of `URL` objects (e.g. `delete
myURL.protocol`, `delete myURL.pathname`, etc) has no effect but will still
return `true`.

