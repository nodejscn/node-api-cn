<!-- YAML
added: v15.6.0
-->

* `name` {string}
* `options` {Object}
  * `subject` {string} `'always'` or `'never'`. **Default:** `'always'`.
  * `wildcards` {boolean} **Default:** `true`.
  * `partialWildcards` {boolean} **Default:** `true`.
  * `multiLabelWildcards` {boolean} **Default:** `false`.
  * `singleLabelSubdomains` {boolean} **Default:** `false`.
* Returns: {string|undefined} Returns `name` if the certificate matches,
  `undefined` if it does not.

Checks whether the certificate matches the given host name.

