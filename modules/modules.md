
> Stability: 3 - Locked

<!--name=module-->

Node.js has a simple module loading system.  In Node.js, files and modules
are in one-to-one correspondence (each file is treated as a separate module).

As an example, consider a file named `foo.js`:

```js
const circle = require('./circle.js');
console.log(`The area of a circle of radius 4 is ${circle.area(4)}`);
```

On the first line, `foo.js` loads the module `circle.js` that is in the same
directory as `foo.js`.

Here are the contents of `circle.js`:

```js
const PI = Math.PI;

exports.area = (r) => PI * r * r;

exports.circumference = (r) => 2 * PI * r;
```

The module `circle.js` has exported the functions `area()` and
`circumference()`.  To add functions and objects to the root of your module,
you can add them to the special `exports` object.

Variables local to the module will be private, because the module is wrapped
in a function by Node.js (see [module wrapper](#modules_the_module_wrapper)).
In this example, the variable `PI` is private to `circle.js`.

If you want the root of your module's export to be a function (such as a
constructor) or if you want to export a complete object in one assignment
instead of building it one property at a time, assign it to `module.exports`
instead of `exports`.

Below, `bar.js` makes use of the `square` module, which exports a constructor:

```js
const square = require('./square.js');
var mySquare = square(2);
console.log(`The area of my square is ${mySquare.area()}`);
```

The `square` module is defined in `square.js`:

```js
// assigning to exports will not modify module, must use module.exports
module.exports = (width) => {
  return {
    area: () => width * width
  };
}
```

The module system is implemented in the `require("module")` module.

