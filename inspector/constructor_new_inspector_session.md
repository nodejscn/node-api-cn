<!-- YAML
added: v8.0.0
-->

Create a new instance of the `inspector.Session` class. The inspector session
needs to be connected through [`session.connect()`][] before the messages
can be dispatched to the inspector backend.

`inspector.Session` is an [`EventEmitter`][] with the following events:

