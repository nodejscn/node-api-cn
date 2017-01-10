
<!--type=misc-->

Node.js has several modules compiled into the binary.  These modules are
described in greater detail elsewhere in this documentation.

The core modules are defined within Node.js's source and are located in the
`lib/` folder.

Core modules are always preferentially loaded if their identifier is
passed to `require()`.  For instance, `require('http')` will always
return the built in HTTP module, even if there is a file by that name.

