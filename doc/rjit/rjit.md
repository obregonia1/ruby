# RJIT

This document has some tips that might be useful when you work on RJIT.

## Supported platforms

The following platforms are either tested on CI or assumed to work.

* OS: Linux, macOS
* Arch: x86\_64, aarch64, arm64, i686, i386

### Not supported

The RJIT support for the following platforms is no longer maintained.

* OS: Windows (mswin, MinGW), Solaris
* Arch: SPARC, s390x

## Developing RJIT

### Bindgen

If you see an "RJIT bindgen" GitHub Actions failure, please commit the `git diff` shown on the failed job.

For doing the same thing locally, run `make rjit-bindgen` after installing libclang.
macOS seems to have libclang by default. On Ubuntu, you can install it with `apt install libclang1`.

### Always run make install

Always run `make install` before running RJIT. It could easily cause a SEGV if you don't.
RJIT looks for the installed header for security reasons.

### --rjit-debug vs --rjit-debug=-ggdb3

`--rjit-debug=[flags]` allows you to specify arbitrary flags while keeping other compiler flags like `-O3`,
which is useful for profiling benchmarks.

`--rjit-debug` alone, on the other hand, disables `-O3` and adds debug flags.
If you're debugging RJIT, what you need to use is not `--rjit-debug=-ggdb3` but `--rjit-debug`.