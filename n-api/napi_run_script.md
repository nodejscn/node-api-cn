<!-- YAML
added: v8.5.0
napiVersion: 1
-->

```c
NAPI_EXTERN napi_status napi_run_script(napi_env env,
                                        napi_value script,
                                        napi_value* result);
```

* `[in] env`: The environment that the API is invoked under.
* `[in] script`: A JavaScript string containing the script to execute.
* `[out] result`: The value resulting from having executed the script.

This function executes a string of JavaScript code and returns its result with
the following caveats:

* Unlike `eval`, this function does not allow the script to access the current
  lexical scope, and therefore also does not allow to access the
  [module scope][], meaning that pseudo-globals such as `require` will not be
  available.
* The script can access the [global scope][]. Function and `var` declarations
  in the script will be added to the [`global`][] object. Variable declarations
  made using `let` and `const` will be visible globally, but will not be added
  to the [`global`][] object.
* The value of `this` is [`global`][] within the script.

