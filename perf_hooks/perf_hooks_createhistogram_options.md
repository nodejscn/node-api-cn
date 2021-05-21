<!-- YAML
added: v15.9.0
-->

* `options` {Object}
  * `min` {number|bigint} The minimum recordable value. Must be an integer
    value greater than 0. **Default:** `1`.
  * `max` {number|bigint} The maximum recordable value. Must be an integer
    value greater than `min`. **Default:** `Number.MAX_SAFE_INTEGER`.
  * `figures` {number} The number of accuracy digits. Must be a number between
    `1` and `5`. **Default:** `3`.
* Returns {RecordableHistogram}

Returns a {RecordableHistogram}.

