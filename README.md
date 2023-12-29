# crux-ports-crossbuild

Unofficial CRUX's ports to cross build for other architechtures

To use these ports, select a branch (for example 3.7) and download the `crossbuild.httpup` file to `/etc/ports`
```
$ sudo wget -P /etc/ports https://raw.githubusercontent.com/sepen/crux-ports-crossbuild/3.7/crossbuild.httpup
$ sudo ports -u crossbuild
```

The goal of this repo is to maintain a list of ports useful for cross-compilation of different systems,
to facilitate tasks such as compiling kernels for small devices where native compilation is unsustainable or impossible.

If you don't have a CRUX host or if what you are looking for is to obtain a complete toolchain then visit https://github.com/crux-arm and clone the toolchain you need (for example: https://github.com/crux-arm/crux-toolchain-arm-linux-gnueabihf)

Current status:

| GNU Triplet | Linux Headers | Binutils | Glibc | GCC | Description |
|-------------|---------------|----------|-------| ----|-------------|
| arm-linux-gnu | 2.6.32 | 2.23.1 | 2.11 | 4.4.2 | Using the "old" and obsolete ABI (OABI). Also known as "noeabi" |
| arm-linux-gnueabi | - | - | - | - | Using the "new" ABI (EABI), supported on armv4t and higher. Also known as "armel" |
| arm-linux-gnueabihf | - | - | - | - | Hard-float version of the "new" ABI (EABI), targeting armv7 and up |
| aarch64-linux-gnu | - | - | - | - | 64-bit armv8 architecture |

