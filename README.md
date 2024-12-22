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

    # The tool chain to use. Only used on Windows. Must be 'vc' for Visual C++
    # or 'msys2' for MingW64. Required.
    toolchain: 'vc'

    # The target architecture. Only used on Windows. Must be 'x64'
    # or 'x86' if toolchain is 'vc' and 'mingw32' or 'mingw64' if
    # toolchain is 'msys2'. Required.
    target-arch: 'x64'

```

Invoking the action will result in a Tcl installation corresponding to the
specified tag. Additionally, the following environment variables are set
for use by the steps in the caller.

- `TCLDIR` set to the location of the directory where Tcl is installed
- `TCLEXTRASDIR` set to the directory where extensions may build any additional
  libraries that may be required.
- `IMAGEOS` set to the runner image (e.g. `ubuntu20`). This is supposed to be
  already available in the `env` context but is not seen by the caching code
  so it is set explicitly.

Most extensions will only care about `TCLDIR`.

See the previously mentioned templates for example usage.
