
Paths specified using a {Buffer} are useful primarily on certain POSIX
operating systems that treat file paths as opaque byte sequences. On such
systems, it is possible for a single file path to contain sub-sequences that
use multiple character encodings. As with string paths, {Buffer} paths may
be relative or absolute:

Example using an absolute path on POSIX:

```mjs
import { open } from 'fs/promises';

let fd;
try {
  fd = await open(Buffer.from('/open/some/file.txt'), 'r');
  // Do something with the file
} finally {
  await fd.close();
}
```

