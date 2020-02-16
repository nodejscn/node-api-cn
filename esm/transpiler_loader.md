
Sources that are in formats Node.js doesn’t understand can be converted into
JavaScript using the [`transformSource` hook][]. Before that hook gets called,
however, other hooks need to tell Node.js not to throw an error on unknown file
types; and to tell Node.js how to load this new file type.

This is obviously less performant than transpiling source files before running
Node.js; a transpiler loader should only be used for development and testing
purposes.

```js
// coffeescript-loader.mjs
import { URL, pathToFileURL } from 'url';
import CoffeeScript from 'coffeescript';

const baseURL = pathToFileURL(`${process.cwd()}/`).href;

// CoffeeScript files end in .coffee, .litcoffee or .coffee.md.
const extensionsRegex = /\.coffee$|\.litcoffee$|\.coffee\.md$/;

export function resolve(specifier, context, defaultResolve) {
  const { parentURL = baseURL } = context;

  // Node.js normally errors on unknown file extensions, so return a URL for
  // specifiers ending in the CoffeeScript file extensions.
  if (extensionsRegex.test(specifier)) {
    return {
      url: new URL(specifier, parentURL).href
    };
  }

  // Let Node.js handle all other specifiers.
  return defaultResolve(specifier, context, defaultResolve);
}

export function getFormat(url, context, defaultGetFormat) {
  // Now that we patched resolve to let CoffeeScript URLs through, we need to
  // tell Node.js what format such URLs should be interpreted as. For the
  // purposes of this loader, all CoffeeScript URLs are ES modules.
  if (extensionsRegex.test(url)) {
    return {
      format: 'module'
    };
  }

  // Let Node.js handle all other URLs.
  return defaultGetFormat(url, context, defaultGetFormat);
}

export function transformSource(source, context, defaultTransformSource) {
  const { url, format } = context;

  if (extensionsRegex.test(url)) {
    return {
      source: CoffeeScript.compile(source, { bare: true })
    };
  }

  // Let Node.js handle all other sources.
  return defaultTransformSource(source, context, defaultTransformSource);
}
```

```coffee
# main.coffee
import { scream } from './scream.coffee'
console.log scream 'hello, world'

import { version } from 'process'
console.log "Brought to you by Node.js version #{version}"
```

```coffee
# scream.coffee
export scream = (str) -> str.toUpperCase()
```

With this loader, running:

```console
node --experimental-loader ./coffeescript-loader.mjs main.coffee
```

Will cause `main.coffee` to be turned into JavaScript after its source code is
loaded from disk but before Node.js executes it; and so on for any `.coffee`,
`.litcoffee` or `.coffee.md` files referenced via `import` statements of any
loaded file.

