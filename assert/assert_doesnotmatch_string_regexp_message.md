<!-- YAML
added: v13.6.0
-->

* `string` {string}
* `regexp` {RegExp}
* `message` {string|Error}

> Stability: 1 - Experimental

Expects the `string` input not to match the regular expression.

This feature is currently experimental and the name might change or it might be
completely removed again.

```js
const assert = require('assert').strict;

assert.doesNotMatch('I will fail', /fail/);
// AssertionError [ERR_ASSERTION]: The input was expected to not match the ...

assert.doesNotMatch(123, /pass/);
// AssertionError [ERR_ASSERTION]: The "string" argument must be of type string.

assert.doesNotMatch('I will pass', /different/);
// OK
```

If the values do match, or if the `string` argument is of another type than
`string`, an [`AssertionError`][] is thrown with a `message` property set equal
to the value of the `message` parameter. If the `message` parameter is
undefined, a default error message is assigned. If the `message` parameter is an
instance of an [`Error`][] then it will be thrown instead of the
[`AssertionError`][].

