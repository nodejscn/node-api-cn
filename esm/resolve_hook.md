
The resolve hook returns the resolved file URL and module format for a
given module specifier and parent file URL:

```js
import { URL, pathToFileURL } from 'url';
const baseURL = pathToFileURL(process.cwd()).href;

/**
 * @param {string} specifier
 * @param {string} parentModuleURL
 * @param {function} defaultResolver
 */
export async function resolve(specifier,
                              parentModuleURL = baseURL,
                              defaultResolver) {
  return {
    url: new URL(specifier, parentModuleURL).href,
    format: 'module'
  };
}
```

The `parentModuleURL` is provided as `undefined` when performing main Node.js
load itself.

The default Node.js ES module resolution function is provided as a third
argument to the resolver for easy compatibility workflows.

In addition to returning the resolved file URL value, the resolve hook also
returns a `format` property specifying the module format of the resolved
module. This can be one of the following:

| `format` | Description |
| --- | --- |
| `'builtin'` | Load a Node.js builtin module |
| `'commonjs'` | Load a Node.js CommonJS module |
| `'dynamic'` | Use a [dynamic instantiate hook][] |
| `'json'` | Load a JSON file |
| `'module'` | Load a standard JavaScript module |
| `'wasm'` | Load a WebAssembly module |

For example, a dummy loader to load JavaScript restricted to browser resolution
rules with only JS file extension and Node.js builtin modules support could
be written:

```js
import path from 'path';
import process from 'process';
import Module from 'module';
import { URL, pathToFileURL } from 'url';

const builtins = Module.builtinModules;
const JS_EXTENSIONS = new Set(['.js', '.mjs']);

const baseURL = pathToFileURL(process.cwd()).href;

/**
 * @param {string} specifier
 * @param {string} parentModuleURL
 * @param {function} defaultResolver
 */
export async function resolve(specifier,
                              parentModuleURL = baseURL,
                              defaultResolver) {
  if (builtins.includes(specifier)) {
    return {
      url: specifier,
      format: 'builtin'
    };
  }
  if (/^\.{0,2}[/]/.test(specifier) !== true && !specifier.startsWith('file:')) {
    // For node_modules support:
    // return defaultResolver(specifier, parentModuleURL);
    throw new Error(
      `imports must begin with '/', './', or '../'; '${specifier}' does not`);
  }
  const resolved = new URL(specifier, parentModuleURL);
  const ext = path.extname(resolved.pathname);
  if (!JS_EXTENSIONS.has(ext)) {
    throw new Error(
      `Cannot load file with non-JavaScript file extension ${ext}.`);
  }
  return {
    url: resolved.href,
    format: 'module'
  };
}
```

With this loader, running:

```console
NODE_OPTIONS='--experimental-modules --loader ./custom-loader.mjs' node x.js
```

would load the module `x.js` as an ES module with relative resolution support
(with `node_modules` loading skipped in this example).

