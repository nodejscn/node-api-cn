
* `emitter` {EventEmitter|Timer} emitter or timer to be added to the domain

Explicitly adds an emitter to the domain.  If any event handlers called by
the emitter throw an error, or if the emitter emits an `'error'` event, it
will be routed to the domain's `'error'` event, just like with implicit
binding.

This also works with timers that are returned from [`setInterval()`][] and
[`setTimeout()`][].  If their callback function throws, it will be caught by
the domain 'error' handler.

If the Timer or EventEmitter was already bound to a domain, it is removed
from that one, and bound to this one instead.

