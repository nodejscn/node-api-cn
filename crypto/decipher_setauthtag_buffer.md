<!-- YAML
added: v1.0.0
-->

When using an authenticated encryption mode (only `GCM` is currently
supported), the `decipher.setAuthTag()` method is used to pass in the
received _authentication tag_. If no tag is provided, or if the cipher text
has been tampered with, [`decipher.final()`][] with throw, indicating that the
cipher text should be discarded due to failed authentication.

