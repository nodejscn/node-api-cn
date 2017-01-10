<!-- YAML
added: v1.0.0
-->

When using an authenticated encryption mode (only `GCM` is currently
supported), the `cipher.getAuthTag()` method returns a [`Buffer`][] containing
the _authentication tag_ that has been computed from the given data.

The `cipher.getAuthTag()` method should only be called after encryption has
been completed using the [`cipher.final()`][] method.

