
* `type` {string} The type of async event.
* `options` {Object}
  * `triggerAsyncId` {number} The ID of the execution context that created this
  async event.  **Default:** `executionAsyncId()`
  * `requireManualDestroy` {boolean} Disables automatic `emitDestroy` when the
  object is garbage collected. This usually does not need to be set (even if
  `emitDestroy` is called manually), unless the resource's asyncId is retrieved
  and the sensitive API's `emitDestroy` is called with it.
  **Default:** `false`

Example usage:

```js
class DBQuery extends AsyncResource {
  constructor(db) {
    super('DBQuery');
    this.db = db;
  }

  getInfo(query, callback) {
    this.db.get(query, (err, data) => {
      this.emitBefore();
      callback(err, data);
      this.emitAfter();
    });
  }

  close() {
    this.db = null;
    this.emitDestroy();
  }
}
```

