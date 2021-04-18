Set up GCC
==========

[![Test](https://github.com/egor-tensin/setup-gcc/actions/workflows/test.yml/badge.svg)](https://github.com/egor-tensin/setup-gcc/actions/workflows/test.yml)

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
| platform  | x64     | ✓       | Install the x86_64 toolchain.
|           | *Other* |         | Install the i686 toolchain.
| cygwin    | *Other* | ✓       | Install native binaries.
|           | 1       |         | Install Cygwin packages.
| cc        | 1       | ✓       | Set up `cc`/`c++` executables.
|           | *Other* |         | Don't set up `cc`/`c++`.
| hardlinks | *Other* | ✓       | Cygwin: don't convert any symlinks.
|           | 1       |         | Cygwin: convert symlinks in /usr/bin to hardlinks.

License
-------

Distributed under the MIT License.
See [LICENSE.txt] for details.

[LICENSE.txt]: LICENSE.txt
