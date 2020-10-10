<!-- YAML
added:
 - v12.0.0
 - v10.17.0
-->

By default all unhandled rejections trigger a warning plus a deprecation warning
for the very first unhandled rejection in case no [`unhandledRejection`][] hook
is used.

Using this flag allows to change what should happen when an unhandled rejection
occurs. One of the following modes can be chosen:

* `throw`: Emit [`unhandledRejection`][]. If this hook is not set, raise the
  unhandled rejection as an uncaught exception.
* `strict`: Raise the unhandled rejection as an uncaught exception.
* `warn`: Always trigger a warning, no matter if the [`unhandledRejection`][]
  hook is set or not but do not print the deprecation warning.
* `warn-with-error-code`: Emit [`unhandledRejection`][]. If this hook is not
  set, trigger a warning, and set the process exit code to 1.
* `none`: Silence all warnings.

