Set up GCC
==========

[![Test](https://github.com/egor-tensin/setup-gcc/actions/workflows/test.yml/badge.svg)](https://github.com/egor-tensin/setup-gcc/actions/workflows/test.yml)

This GitHub action sets up GCC in your workflow run.

1. Installs either 32-bit or 64-bit GCC on either Ubuntu or Cygwin.
2. Specify a version to install using the `version` parameter.
2. For installing GCC on Windows please see my action [setup-mingw].

[setup-mingw]: https://github.com/egor-tensin/setup-mingw

Use it in your workflow like this:

    - name: Set up GCC
      uses: egor-tensin/setup-gcc@v1
      with:
        version: latest
        platform: x64

* `latest` is the default value for the `version` parameter and can be omitted.
* `x64` is the default value for the `platform` parameter and can be omitted.
Use `x86` if you want to build 32-bit binaries.
* Set the `cygwin` parameter to `1` to set up GCC inside an existing Cygwin
installation (you can set up Cygwin itself using my action [setup-cygwin]).
* `cc` and `c++` executables are set up, pointing to the `gcc` and `g++`
executables.
Disable this by setting the `cc` parameter to `0`.

[setup-cygwin]: https://github.com/egor-tensin/setup-cygwin

API
---

| Input     | Value   | Default | Description
| --------- | ------- | ------- | -----------
| version   | latest  | ✓       | Install the latest version available in the repository.
|           | *any*   |         | Install a specific version if it's available (see below).
| platform  | x64     | ✓       | Install the x86_64 toolchain.
|           | *any*   |         | Install the i686 toolchain.
| cygwin    | *any*   | ✓       | Install native binaries.
|           | 1       |         | Install Cygwin packages.
| cc        | 1       | ✓       | Set up `cc`/`c++` executables.
|           | *any*   |         | Don't set up `cc`/`c++`.
| hardlinks | *any*   | ✓       | Cygwin: don't convert any symlinks.
|           | 1       |         | Cygwin: convert symlinks in /usr/bin to hardlinks.

Supported versions
------------------

Unless the `version` parameter value is "latest", the ubuntu-toolchain-r/test
PPA is used to make more GCC versions available.
You can pass the version number as the `version` parameter value (`4.8`, `8`,
`9`, etc.), and this action will install the corresponding `g++-VERSION`
package.

The `version` parameter value is not checked for being an available version for
the current distribution.
The supported versions for a particular distribution are those found in the
official repositories & those found in that distribution's series in the PPA.
For example, the supported versions for Bionic & Focal as of July 2021 are
listed below.

| `version` | Bionic | Focal
| --------- | ------ | -----
| 4.8       | ✓      |
| 5         | ✓      |
| 6         | ✓      |
| 7         | ✓      | ✓
| 8         | ✓      | ✓
| 9         | ✓      | ✓
| 10        | ✓      | ✓
| 11        | ✓      | ✓

This table is not definitive; I expect more future versions of GCC to be made
available in the PPA, especially for Focal.

On Cygwin, the `version` parameter is ignored.

License
-------

Distributed under the MIT License.
See [LICENSE.txt] for details.

[LICENSE.txt]: LICENSE.txt
