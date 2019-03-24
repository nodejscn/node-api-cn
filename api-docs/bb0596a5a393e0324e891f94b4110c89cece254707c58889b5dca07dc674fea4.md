<!-- YAML
added: v10.0.0
-->

`util.types` provides a number of type checks for different kinds of built-in
objects. Unlike `instanceof` or `Object.prototype.toString.call(value)`,
these checks do not inspect properties of the object that are accessible from
JavaScript (like their prototype), and usually have the overhead of
calling into C++.

The result generally does not make any guarantees about what kinds of
properties or behavior a value exposes in JavaScript. They are primarily
useful for addon developers who prefer to do type checking in JavaScript.

