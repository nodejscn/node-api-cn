
This option makes the resulting binary link against the ICU library statically,
and includes a subset of ICU data (typically only the English locale) within
the `node` executable.

Functionalities that only require the ICU library itself, such as
[`String.prototype.normalize()`][] and the [WHATWG URL parser][], are fully
supported under `small-icu`. Features that require ICU locale data in addition,
such as [`Intl.DateTimeFormat`][], generally only work with the English locale:

```js
const january = new Date(9e8);
const english = new Intl.DateTimeFormat('en', { month: 'long' });
const spanish = new Intl.DateTimeFormat('es', { month: 'long' });

console.log(english.format(january));
// Prints "January"
console.log(spanish.format(january));
// Prints "M01" on small-icu
// Should print "enero"
```

This mode provides a good balance between features and binary size, and it is
the default behavior if no `--with-intl` flag is passed. The official binaries
are also built in this mode.

