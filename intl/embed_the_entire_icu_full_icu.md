
This option makes the resulting binary link against ICU statically and include
a full set of ICU data. A binary created this way has no further external
dependencies and supports all locales, but might be rather large. This is
the default behavior if no `--with-intl` flag is passed. The official binaries
are also built in this mode.

