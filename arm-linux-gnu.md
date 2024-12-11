# arm-linux-gnu

## Ports Dependency tree

```
gcc-arm-linux-gnu
  glibc-arm-linux-gnu
    static-gcc-arm-linux-gnu
      binutils-arm-linux-gnu
        libmpc-arm-linux-gnu
          libmpfr-arm-linux-gnu
            libgmp-arm-linux-gnu
              kernel-headers-arm-linux-gnu
      kernel-headers-arm-linux-gnu
    make43
    kernel-headers-arm-linux-gnu
```

## Notes about GCC

- GCC 4.7.4 is the last version to support EABI-0 (noeabi) on ARM platforms.
- From GCC 4.8 onward, the toolchain defaults to AAPCS, and support for EABI-0 is removed or no longer actively maintained.
  - https://gcc.gnu.org/gcc-4.7/changes.html

- Support on ARM for the legacy floating-point accelerator (FPA) and the mixed-endian floating-point format that it used has been obsoleted.
- The GCC ports that still use this format have been obsoleted as well.
- Many legacy GCC ports for ARM already provide an alternative that uses the VFP floating-point format.
- The `arm*-*-linux-gnu` ports will be deleted in the next release.
- The configure script requires and additional flag in order to compile:
  > *** Configuration arm-unknown-linux-gnu is obsolete.
  > *** Specify --enable-obsolete to build it anyway.
  > *** Support will be REMOVED in the next major release of GCC,
  > *** unless a maintainer comes forward.


## Notes about Glibc

- EABI-0 (noeabi) support was removed in glibc 2.12 and in the glibc-ports.git repository before this version, making it no longer feasible to use EABI-0 with modern versions of glibc (post-2.11).
- If you need to work with EABI-0 (noeabi), the last supported version of glibc is glibc 2.11.x (and possibly very early glibc 2.12 versions if you manage to find a patched version).
- After glibc 2.12, the glibc project shifted away from supporting EABI-0 entirely.

- Commits where they remove ARM old-ABI support (straightforward parts)
  - https://sourceware.org/git/?p=glibc.git;a=commit;h=5155e70cbe179919d3d10a7b8d91ba9ee775c9fc
  - https://sourceware.org/git/?p=glibc-ports.git;a=commit;h=5155e70cbe179919d3d10a7b8d91ba9ee775c9fc


## Notes about Binutils

- Binutils 2.20 to 2.22 are the best versions for working with EABI-0 (noeabi) support.
- Starting with binutils 2.23, EABI-0 support is no longer a priority and is effectively removed in versions after binutils 2.22.
- If you need to maintain compatibility with EABI-0 in modern systems, using binutils 2.22 or earlier, or building a custom patched toolchain, is generally the best approach

