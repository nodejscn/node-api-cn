<!-- YAML
added: v15.12.0
-->

> Stability: 1 - Experimental

* `key` {any} Any arbitrary, cloneable JavaScript value that can be used as a
  {Map} key.
* `value` {any} Any arbitrary, cloneable JavaScript value that will be cloned
  and passed automatically to all new `Worker` instances. If `value` is passed
  as `undefined`, any previously set value for the `key` will be deleted.

The `worker.setEnvironmentData()` API sets the content of
`worker.getEnvironmentData()` in the current thread and all new `Worker`
instances spawned from the current context.

