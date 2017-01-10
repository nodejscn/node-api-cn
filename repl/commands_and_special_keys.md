
The following special commands are supported by all REPL instances:

* `.break` - When in the process of inputting a multi-line expression, entering
  the `.break` command (or pressing the `<ctrl>-C` key combination) will abort
  further input or processing of that expression.
* `.clear` - Resets the REPL `context` to an empty object and clears any
  multi-line expression currently being input.
* `.exit` - Close the I/O stream, causing the REPL to exit.
* `.help` - Show this list of special commands.
* `.save` - Save the current REPL session to a file:
  `> .save ./file/to/save.js`
* `.load` - Load a file into the current REPL session.
  `> .load ./file/to/load.js`
* `.editor` - Enter editor mode (`<ctrl>-D` to finish, `<ctrl>-C` to cancel)

```js
> .editor
// Entering editor mode (^D to finish, ^C to cancel)
function welcome(name) {
  return `Hello ${name}!`;
}

welcome('Node.js User');

// ^D
'Hello Node.js User!'
>
```

The following key combinations in the REPL have these special effects:

* `<ctrl>-C` - When pressed once, has the same effect as the `.break` command.
  When pressed twice on a blank line, has the same effect as the `.exit`
  command.
* `<ctrl>-D` - Has the same effect as the `.exit` command.
* `<tab>` - When pressed on a blank line, displays global and local(scope)
  variables. When pressed while entering other input, displays relevant
  autocompletion options.

