
* `callback` {Function} The callback function
* Returns: {Function} The bound function

The returned function will be a wrapper around the supplied callback
function.  When the returned function is called, any errors that are
thrown will be routed to the domain's `'error'` event.

