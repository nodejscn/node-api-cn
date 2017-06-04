
<!--type=misc-->

If domains are in use, then all **new** EventEmitter objects (including
Stream objects, requests, responses, etc.) will be implicitly bound to
the active domain at the time of their creation.

Additionally, callbacks passed to lowlevel event loop requests (such as
to fs.open, or other callback-taking methods) will automatically be
bound to the active domain. If they throw, then the domain will catch
the error.

In order to prevent excessive memory usage, Domain objects themselves
are not implicitly added as children of the active domain.  If they
were, then it would be too easy to prevent request and response objects
from being properly garbage collected.

To nest Domain objects as children of a parent Domain they must be explicitly
added.

Implicit binding routes thrown errors and `'error'` events to the
Domain's `'error'` event, but does not register the EventEmitter on the
Domain, so [`domain.dispose()`][] will not shut down the EventEmitter.
Implicit binding only takes care of thrown errors and `'error'` events.

