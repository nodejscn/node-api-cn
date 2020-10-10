<!-- YAML
added: v12.0.0
-->

Disable [runtime allocation of executable memory][jitless]. This may be
required on some platforms for security reasons. It can also reduce attack
surface on other platforms, but the performance impact may be severe.

This flag is inherited from V8 and is subject to change upstream. It may
disappear in a non-semver-major release.

