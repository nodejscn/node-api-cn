
The CommonJS module `require` always treats the files it references as CommonJS.

Using `require` to load an ES module is not supported because ES modules have
asynchronous execution. Instead, use [`import()`][] to load an ES module
from a CommonJS module.

