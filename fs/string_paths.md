
String form paths are interpreted as UTF-8 character sequences identifying
the absolute or relative filename. Relative paths will be resolved relative
to the current working directory as determined by calling `process.cwd()`.

Example using an absolute path on POSIX:

```mjs
import { open } from 'fs/promises';

let fd;
try {
  fd = await open('/open/some/file.txt', 'r');
  // Do something with the file
} finally {
  await fd.close();
}
```

Example using a relative path on POSIX (relative to `process.cwd()`):

```mjs
import { open } from 'fs/promises';

let fd;
try {
  fd = await open('file.txt', 'r');
  // Do something with the file
} finally {
  await fd.close();
}
```

