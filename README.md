# crux-ports-crossbuild

Unofficial CRUX's ports to cross build for other architechtures

To use these ports, select a branch (for example 3.7) and download the `crossbuild.httpup` file to `/etc/ports`
```
$ sudo wget -P /etc/ports https://raw.githubusercontent.com/sepen/crux-ports-crossbuild/3.7/crossbuild.httpup
$ sudo ports -u crossbuild
```

The goal of this repo is to maintain a list of ports useful for cross-compilation for different target systems,
to facilitate tasks such as compiling kernels for small devices where native compilation is unsustainable and/or impossible.

## Targets

| GNU Triplet | Linux Headers | Binutils | Glibc | GCC | Description |
|-------------|---------------|----------|-------| ----|-------------|
| aarch64-linux-gnu | - | - | - | - | Aarch64 - ARMv8-A 64-bit |
| arm-linux-gnueabihf | - | - | - | - | Aarch32 - Hard-float targeting ARMv7 and up |
| arm-linux-gnueabi | 3.2.75 | 2.39 | 2.36 | 12.3.0 | EABI - Using the "new" ABI (EABI), supported on ARMv4t and higher (aka "armel") |
| arm-linux-gnu | 3.1.10 | 2.23.1 | 2.11.3 (kernel >=2.6.0) | 4.7.4 | OABI - Using the "old" and obsolete EABI 0 (aka "noeabi") |

