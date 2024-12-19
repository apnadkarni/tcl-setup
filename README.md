# setup-tcl

This action sets up an environment to build and test Tcl extensions
against a specific build of Tcl. Tcl builds are cached so as to not require
recompilation on every CI run.

See [action.yml](action.yml) for required inputs.

See [tcl-cffi workflows](https://github.com/apnadkarni/tcl-cffi/tree/main/.github/workflows)
for example usage.
