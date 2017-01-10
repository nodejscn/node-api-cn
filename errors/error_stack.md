
Returns a string describing the point in the code at which the `Error` was
instantiated.

For example:

```txt
Error: Things keep happening!
   at /home/gbusey/file.js:525:2
   at Frobnicator.refrobulate (/home/gbusey/business-logic.js:424:21)
   at Actor.<anonymous> (/home/gbusey/actors.js:400:8)
   at increaseSynergy (/home/gbusey/actors.js:701:6)
```

The first line is formatted as `<error class name>: <error message>`, and
is followed by a series of stack frames (each line beginning with "at ").
Each frame describes a call site within the code that lead to the error being
generated. V8 attempts to display a name for each function (by variable name,
function name, or object method name), but occasionally it will not be able to
find a suitable name. If V8 cannot determine a name for the function, only
location information will be displayed for that frame. Otherwise, the
determined function name will be displayed with location information appended
in parentheses.

It is important to note that frames are **only** generated for JavaScript
functions. If, for example, execution synchronously passes through a C++ addon
function called `cheetahify`, which itself calls a JavaScript function, the
frame representing the `cheetahify` call will **not** be present in the stack
traces:

```js
const cheetahify = require('./native-binding.node');

function makeFaster() {
  // cheetahify *synchronously* calls speedy.
  cheetahify(function speedy() {
    throw new Error('oh no!');
  });
}

makeFaster(); // will throw:
  // /home/gbusey/file.js:6
  //     throw new Error('oh no!');
  //           ^
  // Error: oh no!
  //     at speedy (/home/gbusey/file.js:6:11)
  //     at makeFaster (/home/gbusey/file.js:5:3)
  //     at Object.<anonymous> (/home/gbusey/file.js:10:1)
  //     at Module._compile (module.js:456:26)
  //     at Object.Module._extensions..js (module.js:474:10)
  //     at Module.load (module.js:356:32)
  //     at Function.Module._load (module.js:312:12)
  //     at Function.Module.runMain (module.js:497:10)
  //     at startup (node.js:119:16)
  //     at node.js:906:3
```

The location information will be one of:

* `native`, if the frame represents a call internal to V8 (as in `[].forEach`).
* `plain-filename.js:line:column`, if the frame represents a call internal
   to Node.js.
* `/absolute/path/to/file.js:line:column`, if the frame represents a call in
  a user program, or its dependencies.

The string representing the stack trace is lazily generated when the
`error.stack` property is **accessed**.

The number of frames captured by the stack trace is bounded by the smaller of
`Error.stackTraceLimit` or the number of available frames on the current event
loop tick.

System-level errors are generated as augmented `Error` instances, which are
detailed [here](#errors_system_errors).

