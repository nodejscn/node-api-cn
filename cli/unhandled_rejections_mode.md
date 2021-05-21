<!-- YAML
added:
  - v12.0.0
  - v10.17.0
changes:
  - version: v15.0.0
    pr-url: https://github.com/nodejs/node/pull/33021
    description: Changed default mode to `throw`. Previously, a warning was
                 emitted.
-->

Using this flag allows to change what should happen when an unhandled rejection
occurs. One of the following modes can be chosen:

* `throw`: Emit [`unhandledRejection`][]. If this hook is not set, raise the
  unhandled rejection as an uncaught exception. This is the default.
* `strict`: Raise the unhandled rejection as an uncaught exception.
* `warn`: Always trigger a warning, no matter if the [`unhandledRejection`][]
  hook is set or not but do not print the deprecation warning.
* `warn-with-error-code`: Emit [`unhandledRejection`][]. If this hook is not
  set, trigger a warning, and set the process exit code to 1.
* `none`: Silence all warnings.

