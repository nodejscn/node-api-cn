
<!-- type=misc -->

想要获得调用 `require()` 时加载的确切的文件名，使用 `require.resolve()` 函数。

综上所述，以下用伪代码描述的高级算法，解释 `resolve()` 做了些什么：

```txt
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
4. LOAD_SELF_REFERENCE(X, dirname(Y))
5. LOAD_NODE_MODULES(X, dirname(Y))
6. THROW "not found"

LOAD_AS_FILE(X)
1. If X is a file, load X as JavaScript text.  STOP
2. If X.js is a file, load X.js as JavaScript text.  STOP
3. If X.json is a file, parse X.json to a JavaScript Object.  STOP
4. If X.node is a file, load X.node as binary addon.  STOP

LOAD_INDEX(X)
1. If X/index.js is a file, load X/index.js as JavaScript text.  STOP
2. If X/index.json is a file, parse X/index.json to a JavaScript object. STOP
3. If X/index.node is a file, load X/index.node as binary addon.  STOP

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
   a. LOAD_AS_FILE(DIR/X)
   b. LOAD_AS_DIRECTORY(DIR/X)

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
4. If the name in `package.json` isn't a prefix of X, throw "not found".
5. Otherwise, resolve the remainder of X relative to this package as if it
   was loaded via `LOAD_NODE_MODULES` with a name in `package.json`.
```

Node.js 允许通过 `LOAD_NODE_MODULES` 加载的包显式地声明要导入的文件路径以及如何解析它们。 
这扩展了使用 `main` 字段已经拥有的控件包。 

启用此功能后，`LOAD_NODE_MODULES` 将更改为：


```txt
LOAD_NODE_MODULES(X, START)
1. let DIRS = NODE_MODULES_PATHS(START)
2. for each DIR in DIRS:
   a. let FILE_PATH = RESOLVE_BARE_SPECIFIER(DIR, X)
   b. LOAD_AS_FILE(FILE_PATH)
   c. LOAD_AS_DIRECTORY(FILE_PATH)

RESOLVE_BARE_SPECIFIER(DIR, X)
1. Try to interpret X as a combination of name and subpath where the name
   may have a @scope/ prefix and the subpath begins with a slash (`/`).
2. If X matches this pattern and DIR/name/package.json is a file:
   a. Parse DIR/name/package.json, and look for "exports" field.
   b. If "exports" is null or undefined, GOTO 3.
   c. If "exports" is an object with some keys starting with "." and some keys
      not starting with ".", throw "invalid config".
   d. If "exports" is a string, or object with no keys starting with ".", treat
      it as having that value as its "." object property.
   e. If subpath is "." and "exports" does not have a "." entry, GOTO 3.
   f. Find the longest key in "exports" that the subpath starts with.
   g. If no such key can be found, throw "not found".
   h. let RESOLVED_URL =
        PACKAGE_EXPORTS_TARGET_RESOLVE(pathToFileURL(DIR/name), exports[key],
        subpath.slice(key.length), ["node", "require"]), as defined in the ESM
        resolver.
   i. return fileURLToPath(RESOLVED_URL)
3. return DIR/X
```

只有当加载上面定义的包名时才会遵守 `"exports"`。 
嵌套目录和包中的任何 `"exports"` 值必须由负责名称的 `package.json` 声明。

