
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
4. LOAD_NODE_MODULES(X, dirname(Y))
5. THROW "not found"

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
```

如果启用了 `--experimental-exports`，则 node 允许通过 `LOAD_NODE_MODULES` 加载的包显式地声明要导入的文件路径以及如何解析它们。 
这扩展了使用 `main` 字段已经拥有的控件包。 
启用此功能后，`LOAD_NODE_MODULES` 将更改如下：


```txt
LOAD_NODE_MODULES(X, START)
1. let DIRS = NODE_MODULES_PATHS(START)
2. for each DIR in DIRS:
   a. let FILE_PATH = RESOLVE_BARE_SPECIFIER(DIR, X)
   a. LOAD_AS_FILE(FILE_PATH)
   b. LOAD_AS_DIRECTORY(FILE_PATH)

RESOLVE_BARE_SPECIFIER(DIR, X)
1. Try to interpret X as a combination of name and subpath where the name
   may have a @scope/ prefix and the subpath begins with a slash (`/`).
2. If X matches this pattern and DIR/name/package.json is a file:
   a. Parse DIR/name/package.json, and look for "exports" field.
   b. If "exports" is null or undefined, GOTO 3.
   c. Find the longest key in "exports" that the subpath starts with.
   d. If no such key can be found, throw "not found".
   e. If the key matches the subpath entirely, return DIR/name/${exports[key]}.
   f. If either the key or exports[key] do not end with a slash (`/`),
      throw "not found".
   g. Return DIR/name/${exports[key]}${subpath.slice(key.length)}.
3. return DIR/X
```

只有当加载上面定义的包名时才会遵守 `"exports"`。 
嵌套目录和包中的任何 `"exports"` 值必须由负责名称的 `package.json` 声明。

