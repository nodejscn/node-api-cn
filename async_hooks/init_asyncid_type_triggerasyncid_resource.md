
* `asyncId` {number} a unique ID for the async resource
* `type` {string} the type of the async resource
* `triggerAsyncId` {number} the unique ID of the async resource in whose
  execution context this async resource was created
* `resource` {Object} reference to the resource representing the async operation,
  needs to be released during _destroy_

Called when a class is constructed that has the _possibility_ to emit an
asynchronous event. This _does not_ mean the instance must call
`before`/`after` before `destroy` is called, only that the possibility
exists.

This behavior can be observed by doing something like opening a resource then
closing it before the resource can be used. The following snippet demonstrates
this.

```js
require('net').createServer().listen(function() { this.close(); });
// OR
clearTimeout(setTimeout(() => {}, 10));
```

Every new resource is assigned a unique ID.

