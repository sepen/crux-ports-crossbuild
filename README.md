# crux-ports-crossbuild

Unofficial CRUX's ports to cross build for other architechtures

To use these ports, download the `crossbuild.httpup` file to `/etc/ports`
```
$ sudo wget -P /etc/ports https://raw.githubusercontent.com/sepen/crux-ports-crossbuild/main/crossbuild.httpup
$ sudo ports -u crossbuild
```

| GNU Triplet | Linux Headers | Binutils | Glibc | GCC | Description |
|-------------|---------------|----------|-------| ----|-------------|
| arm-linux-gnu | 2.6.32 | 2.23.1 | 2.11 | 4.4.2 | Using the "old" and obsolete ABI (OABI). Also known as "noeabi" |
| arm-linux-gnueabi | - | - | - | - | Using the "new" ABI (EABI), supported on armv4t and higher. Also known as "armel" |
| arm-linux-gnueabihf | - | - | - | - | Hard-float version of the "new" ABI (EABI), targeting armv7 and up |
| aarch64-linux-gnu | - | - | - | - | 64-bit armv8 architecture |

