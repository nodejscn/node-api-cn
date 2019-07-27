<!-- YAML
added: v12.0.0
-->

By default all unhandled rejections trigger a warning plus a deprecation warning
for the very first unhandled rejection in case no [`unhandledRejection`][] hook
is used.

Using this flag allows to change what should happen when an unhandled rejection
occurs. One of three modes can be chosen:

* `strict`: Raise the unhandled rejection as an uncaught exception.
* `warn`: Always trigger a warning, no matter if the [`unhandledRejection`][]
  hook is set or not but do not print the deprecation warning.
* `none`: Silence all warnings.

