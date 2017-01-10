
This object is created internally and is returned from [`setTimeout()`][] and
[`setInterval()`][]. It can be passed to [`clearTimeout()`][] or
[`clearInterval()`][] (respectively) in order to cancel the scheduled actions.

By default, when a timer is scheduled using either [`setTimeout()`][] or
[`setInterval()`][], the Node.js event loop will continue running as long as the
timer is active. Each of the `Timeout` objects returned by these functions
export both `timeout.ref()` and `timeout.unref()` functions that can be used to
control this default behavior.

