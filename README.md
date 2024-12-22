# crux-ports-crossbuild

Unofficial CRUX's ports to cross build for other architechtures

To use these ports, select a branch (for example 3.7) and download the `crossbuild.httpup` file to `/etc/ports`
```
$ sudo wget -P /etc/ports https://raw.githubusercontent.com/sepen/crux-ports-crossbuild/3.7/crossbuild.httpup
$ sudo ports -u crossbuild
```
> Note: The version number 3.7 indicates that the ports can be built against a CRUX 3.7 base system.


## Targets

The goal of this repo is to maintain a list of ports useful for cross-compilation for different target systems,
to facilitate tasks such as compiling kernels for small devices where native compilation is unsustainable and/or impossible.

Available targets are:

| Arch  | GNU Triplet           | Binutils | GlibC  | GCC    | Linux Headers | Minimum Kernel |
| --.-: | --------------------: | :------: | :----: | :----: | :-----------: | :------------: |
| arm64 | `aarch64-linux-gnu`   | -        | -      | -      | -             | -              |
| armhf | `arm-linux-gnueabihf` | 2.39     | 2.36   | 12.4.0 | 5.15.55       | 2.6.32         |
| armel | `arm-linux-gnueabi`   | -        | -      | -      | -             | -              |
| armv4 | `arm-linux-gnu`       | 2.23.1   | 2.11.3 | 4.7.4  | 3.1.10        | 2.6.0          |
