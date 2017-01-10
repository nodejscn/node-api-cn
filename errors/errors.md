
<!--type=misc-->

Applications running in Node.js will generally experience four categories of
errors:

- Standard JavaScript errors such as:
  - {EvalError} : thrown when a call to `eval()` fails.
  - {SyntaxError} : thrown in response to improper JavaScript language
    syntax.
  - {RangeError} : thrown when a value is not within an expected range
  - {ReferenceError} : thrown when using undefined variables
  - {TypeError} : thrown when passing arguments of the wrong type
  - {URIError} : thrown when a global URI handling function is misused.
- System errors triggered by underlying operating system constraints such
  as attempting to open a file that does not exist, attempting to send data
  over a closed socket, etc;
- And User-specified errors triggered by application code.
- Assertion Errors are a special class of error that can be triggered whenever
  Node.js detects an exceptional logic violation that should never occur. These
  are raised typically by the `assert` module.

All JavaScript and System errors raised by Node.js inherit from, or are
instances of, the standard JavaScript {Error} class and are guaranteed
to provide *at least* the properties available on that class.

