
<!-- type=misc -->

想要获得调用 `require()` 时加载的确切的文件名，使用 `require.resolve()` 函数。

综上所述，以下用伪代码描述的高级算法，解释 `resolve()` 做了些什么：

```text
require(X) from module at path Y
1. If X is a core module,
   a. return the core module
   b. STOP
2. If X begins with '/'
   a. set Y to be the filesystem root
3. If X begins with './' or '/' or '../'
   a. LOAD_AS_FILE(Y + X)
   b. LOAD_AS_DIRECTORY(Y + X)
   c. THROW "not found"
4. If X begins with '#'
   a. LOAD_INTERAL_IMPORT(X, Y)
4. LOAD_SELF_REFERENCE(X, Y)
5. LOAD_NODE_MODULES(X, dirname(Y))
6. THROW "not found"

LOAD_AS_FILE(X)
1. If X is a file, load X as its file extension format. STOP
2. If X.js is a file, load X.js as JavaScript text. STOP
3. If X.json is a file, parse X.json to a JavaScript Object. STOP
4. If X.node is a file, load X.node as binary addon. STOP

LOAD_INDEX(X)
1. If X/index.js is a file, load X/index.js as JavaScript text. STOP
2. If X/index.json is a file, parse X/index.json to a JavaScript object. STOP
3. If X/index.node is a file, load X/index.node as binary addon. STOP

LOAD_AS_DIRECTORY(X)
1. If X/package.json is a file,
   a. Parse X/package.json, and look for "main" field.
   b. If "main" is a falsy value, GOTO 2.
   c. let M = X + (json main field)
   d. LOAD_AS_FILE(M)
   e. LOAD_INDEX(M)
   f. LOAD_INDEX(X) DEPRECATED
   g. THROW "not found"
2. LOAD_INDEX(X)

LOAD_NODE_MODULES(X, START)
1. let DIRS = NODE_MODULES_PATHS(START)
2. for each DIR in DIRS:
   a. LOAD_PACKAGE_EXPORTS(DIR, X)
   b. LOAD_AS_FILE(DIR/X)
   c. LOAD_AS_DIRECTORY(DIR/X)

NODE_MODULES_PATHS(START)
1. let PARTS = path split(START)
2. let I = count of PARTS - 1
3. let DIRS = [GLOBAL_FOLDERS]
4. while I >= 0,
   a. if PARTS[I] = "node_modules" CONTINUE
   b. DIR = path join(PARTS[0 .. I] + "node_modules")
   c. DIRS = DIRS + DIR
   d. let I = I - 1
5. return DIRS

LOAD_SELF_REFERENCE(X, START)
1. Find the closest package scope to START.
2. If no scope was found, return.
3. If the `package.json` has no "exports", return.
4. If the name in `package.json` is a prefix of X, then
   a. Load the remainder of X relative to this package as if it was
      loaded via `LOAD_NODE_MODULES` with a name in `package.json`.

LOAD_PACKAGE_EXPORTS(DIR, X)
1. Try to interpret X as a combination of name and subpath where the name
   may have a @scope/ prefix and the subpath begins with a slash (`/`).
2. If X does not match this pattern or DIR/name/package.json is not a file,
   return.
3. Parse DIR/name/package.json, and look for "exports" field.
4. If "exports" is null or undefined, return.
5. If "exports" is an object with some keys starting with "." and some keys
  not starting with ".", throw "invalid config".
6. If "exports" is a string, or object with no keys starting with ".", treat
  it as having that value as its "." object property.
7. If subpath is "." and "exports" does not have a "." entry, return.
8. Find the longest key in "exports" that the subpath starts with.
9. If no such key can be found, throw "not found".
10. let RESOLVED =
    fileURLToPath(PACKAGE_EXPORTS_TARGET_RESOLVE(pathToFileURL(DIR/name),
    exports[key], subpath.slice(key.length), ["node", "require"])), as defined
    in the ESM resolver.
11. If key ends with "/":
    a. LOAD_AS_FILE(RESOLVED)
    b. LOAD_AS_DIRECTORY(RESOLVED)
12. Otherwise
   a. If RESOLVED is a file, load it as its file extension format. STOP
13. Throw "not found"

LOAD_INTERNAL_IMPORT(X, START)
1. Find the closest package scope to START.
2. If no scope was found or the `package.json` has no "imports", return.
3. let RESOLVED =
  fileURLToPath(PACKAGE_INTERNAL_RESOLVE(X, pathToFileURL(START)), as defined
  in the ESM resolver.
4. If RESOLVED is not a valid file, throw "not found"
5. Load RESOLVED as its file extension format. STOP
```

