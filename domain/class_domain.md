
The Domain class encapsulates the functionality of routing errors and
uncaught exceptions to the active Domain object.

Domain is a child class of [`EventEmitter`][].  To handle the errors that it
catches, listen to its `'error'` event.

