
* {any}

If the `module.status` is `'errored'`, this property contains the exception
thrown by the module during evaluation. If the status is anything else,
accessing this property will result in a thrown exception.

The value `undefined` cannot be used for cases where there is not a thrown
exception due to possible ambiguity with `throw undefined;`.

Corresponds to the `[[EvaluationError]]` field of [Cyclic Module Record][]s
in the ECMAScript specification.

