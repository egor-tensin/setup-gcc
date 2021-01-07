Set up GCC
==========

[![Test](https://github.com/egor-tensin/setup-gcc/workflows/Test/badge.svg)](https://github.com/egor-tensin/setup-gcc/actions?query=workflow%3ATest)

This is a GitHub action that sets up GCC in your workflow run.

1. Installs either 32-bit or 64-bit GCC on either Ubuntu or Cygwin.
2. For installing GCC on Windows please see my action [setup-mingw].

[setup-mingw]: https://github.com/egor-tensin/setup-mingw

Use it in your workflow like this:

    - name: Set up GCC
      uses: egor-tensin/setup-gcc@v1
      with:
        platform: x64

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
| platform  | x64     | Yes     | Install the x86_64 toolchain.
|           | *Other* | No      | Install the i686 toolchain.
| cygwin    | 1       | No      | Install Cygwin packages.
|           | *Other* | Yes     | Install native binaries.
| cc        | 1       | Yes     | Set up `cc`/`c++` executables.
|           | *Other* | No      | Don't set up `cc`/`c++`.
| hardlinks | *Other* | Yes     | Cygwin: don't convert any symlinks.
|           | 1       | No      | Cygwin: convert symlinks in /usr/bin to hardlinks.

License
-------

Distributed under the MIT License.
See [LICENSE.txt] for details.

[LICENSE.txt]: LICENSE.txt
