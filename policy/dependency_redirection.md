
An application may need to ship patched versions of modules or to prevent
modules from allowing all modules access to all other modules. Redirection
can be used by intercepting attempts to load the modules wishing to be
replaced.

```json
{
  "builtins": [],
  "resources": {
    "./app/checked.js": {
      "dependencies": {
        "fs": true,
        "os": "./app/node_modules/alt-os"
      }
    }
  }
}
```

The dependencies are keyed by the requested string specifier and have values
of either `true` or a string pointing to a module that will be resolved.

The specifier string does not perform any searching and must match exactly
what is provided to the `require()`. Therefore, multiple specifiers may be
needed in the policy if `require()` uses multiple different strings to point
to the same module (such as excluding the extension).

If the value of the redirection is `true` the default searching algorithms will
be used to find the module.

If the value of the redirection is a string, it will be resolved relative to
the manifest and then immediately be used without searching.

Any specifier string that is `require()`ed and not listed in the dependencies
will result in an error according to the policy.

Redirection will not prevent access to APIs through means such as direct access
to `require.cache` and/or through `module.constructor` which allow access to
loading modules. Policy redirection only affect specifiers to `require()`.
Other means such as to prevent undesired access to APIs through variables are
necessary to lock down that path of loading modules.

A boolean value of `true` for the dependencies map can be specified to allow a
module to load any specifier without redirection. This can be useful for local
development and may have some valid usage in production, but should be used
only with care after auditing a module to ensure its behavior is valid.

