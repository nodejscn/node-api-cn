
Take care when launching worker threads from preload scripts (scripts loaded
and run using the `-r` command line flag). Unless the `execArgv` option is
explicitly set, new Worker threads automatically inherit the command line flags
from the running process and will preload the same preload scripts as the main
thread. If the preload script unconditionally launches a worker thread, every
thread spawned will spawn another until the application crashes.





























































