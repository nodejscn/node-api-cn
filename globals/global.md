<!-- YAML
added: v0.1.27
-->

<!-- type=global -->

* {Object} The global namespace object.

In browsers, the top-level scope is the global scope. That means that in
browsers if you're in the global scope `var something` will define a global
variable. In Node.js this is different. The top-level scope is not the global
scope; `var something` inside an Node.js module will be local to that module.

