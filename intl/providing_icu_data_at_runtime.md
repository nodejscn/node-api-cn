
If the `small-icu` option is used, one can still provide additional locale data
at runtime so that the JS methods would work for all ICU locales. Assuming the
data file is stored at `/some/directory`, it can be made available to ICU
through either:

* The [`NODE_ICU_DATA`][] environmental variable:

  ```shell
  env NODE_ICU_DATA=/some/directory node
  ```

* The [`--icu-data-dir`][] CLI parameter:

  ```shell
  node --icu-data-dir=/some/directory
  ```

(If both are specified, the `--icu-data-dir` CLI parameter takes precedence.)

ICU is able to automatically find and load a variety of data formats, but the
data must be appropriate for the ICU version, and the file correctly named.
The most common name for the data file is `icudt5X[bl].dat`, where `5X` denotes
the intended ICU version, and `b` or `l` indicates the system's endianness.
Check ["ICU Data"][] article in the ICU User Guide for other supported formats
and more details on ICU data in general.

The [full-icu][] npm module can greatly simplify ICU data installation by
detecting the ICU version of the running `node` executable and downloading the
appropriate data file. After installing the module through `npm i full-icu`,
the data file will be available at `./node_modules/full-icu`. This path can be
then passed either to `NODE_ICU_DATA` or `--icu-data-dir` as shown above to
enable full `Intl` support.

