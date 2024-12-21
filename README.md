# tcl-setup

This action sets up an environment to build and test Tcl extensions
against a specified build of Tcl. Commonly used in conjunction with the
[tcl-build-extension](https://github.com/apnadkarni/tcl-build-extension)
action which builds Tcl extensions and [Tcl workflow templates].

Tcl builds are cached so as to not require recompilation on every CI run.

# Usage

Example:

```yaml
- name: Setup Tcl
  uses: apnadkarni/tcl-setup@v1
  with:
    # The Tcl repository GIT tag or branch identifying the Tcl version
    # against which the extension is to be built. Required.
    tcl-tag: 'main'

    # The target architecture. Only used on Windows. Must be 'x64'
    # or 'x86'. Optional, defaults to 'x64'.
    target-arch: 'x64'

    # The tool chain to use. Only used on Windows. Must be 'vc' for Visual C++
    # or 'mingw64' for MingW64. Optional, defaults to 'vc`.
    toolchain: 'vc'
```

Invoking the action will result in a Tcl installation corresponding to the
specified tag. The location of the directory is stored in the `TCLDIR` environment
variable for use by subsequent actions. The action also sets the `TClEXTRASDIR`
environment variable to the location where any additional libraries required
by the extension should be installed.

See [tcl-csv workflows](https://github.com/apnadkarni/tcl-csv/tree/main/.github/workflows)
for example usage.
