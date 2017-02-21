
> Stability: 0 - Deprecated.  Please recover from failed IO actions
> explicitly via error event handlers set on the domain.

Once `dispose` has been called, the domain will no longer be used by callbacks
bound into the domain via `run`, `bind`, or `intercept`, and a `'dispose'` event
is emitted.

