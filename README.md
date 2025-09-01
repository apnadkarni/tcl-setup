# tcl-setup v2

*Note: tcl-setup v2 is not compatible with version
[v1](https://github.com/apnadkarni/tcl-setup/blob/v1/README.md).*

This action sets up an environment to build and test Tcl and Tk extensions
against a specified build of Tcl and Tk. Commonly used in conjunction with the
[tcl-build-extension](https://github.com/apnadkarni/tcl-build-extension)
action which builds Tcl extensions and
the [workflow templates](https://github.com/apnadkarni/tcl-extension-template/tree/main/.github/workflows) from
[Tcl extension template](https://github.com/apnadkarni/tcl-extension-template).

The Tcl builds are cached so as to not require recompilation on every CI run.

# Usage

Example:

```yaml
- name: Setup Tcl
  uses: apnadkarni/tcl-setup@v2
  with:
    # The Tcl repository GIT tag or branch identifying the Tcl version
    # against which the extension is to be built. Required.
    # Examples: main, core-9-0-0, core-8-6-branch etc.
    tcl-tag: 'main'

    # The Tk repository GIT tag or branch identifying the Tk version
    # against which the extension is to be built. Optional. Omit if the
    # extension is not a Tk extension. Currently not supported on macOS.
    tk-tag: 'main'

    # The tool chain to use. Only used on Windows. Must be 'vc' for Visual C++
    # or 'msys2' for MingW64. Required on Windows.
    toolchain: 'vc'

    # The target architecture. Only used on Windows. Must be 'x64'
    # or 'x86' if toolchain is 'vc' and 'mingw32' or 'mingw64' if
    # toolchain is 'msys2'. Required on Windows.
    target-arch: 'x64'
```

Invoking the action will result in a Tcl installation corresponding to the
specified tag. Additionally, the following environment variables are set
for use by the steps in the caller if needed.

| Name | Description |
| ---- | ------------|
| IMAGEOS         | The runner image identifier, e.g. `ubuntu22`. |
| TCLGA_TRIPLET   | A value is composed from the OS image, compiler toolchain and architecture used identify build configurations. Callers may use this for purposes of caching other dependencies that are based OS, compiler and architecture. |
| TCLGA_SUBDIR    | A value composed from `TCLGA_TRIPLET` along with the Tcl and Tk repository tags. Callers may use this for purposes of caching other dependencies that are based on the Tcl and Tk versions in addition to OS, compiler and architecture. |
| TCLGA_INSTALL   | Path to the directory where Tcl is installed. |
| TCLGA_TCLSOURCE | The root of the Tcl source directory. |
| TCLGA_TKSOURCE  | The root of the Tk source directory. |
| TCLGA_EXTRAS    | The directory where extensions may build any additional thirdparty libraries that may be required. This is based on `TCLGA_TRIPLET` and independent of the Tcl and Tk tags. |

See the [workflow templates](https://github.com/apnadkarni/tcl-extension-template/tree/main/.github/workflows)
that you can customize for your extension. In most cases, the workflows will
work with minimal or no changes.
