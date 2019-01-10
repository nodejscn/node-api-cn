<!-- YAML
added: v10.0.0
-->

The `Tracing` object is used to enable or disable tracing for sets of
categories. Instances are created using the `trace_events.createTracing()`
method.

When created, the `Tracing` object is disabled. Calling the
`tracing.enable()` method adds the categories to the set of enabled trace event
categories. Calling `tracing.disable()` will remove the categories from the
set of enabled trace event categories.

