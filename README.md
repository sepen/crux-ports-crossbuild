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

| GNU Triplet           | Binutils | GlibC  | GCC    | Linux Headers | Minimum Kernel |
| --------------------: | :------: | :----: | :----: | :-----------: | :------------: |
| `aarch64-linux-gnu`   | -        | -      | -      | -             | -              |
| `arm-linux-gnueabihf` | 2.39     | 2.36   | 12.4.0 | 5.15.55       | 2.6.32         |
| `arm-linux-gnueabi`   | -        | -      | -      | -             | -              |
| `arm-linux-gnu`       | 2.23.1   | 2.11.3 | 4.7.4  | 3.1.10        | 2.6.0          |


## Setting Up Cross Tools

Cross-compiling for a given target (e.g: `arm-linux-gnueabihf`) requires to install some packages and setup some environment variables:

1. Install a cross-compiler and all its dependencies:

   ```bash
   sudo prt-get depinst gcc-arm-linux-gnueabihf
   ```

2. Add `bin` directory to `PATH`:

   After installing everythin you need to add the bin directory where cross tools are located to your PATH so you can use the ARM tools from anywhere.
   ```bash
   export PATH=$PATH:/usr/arm-linux-gnueabihf/bin
   ```

4. Set cross-compilation variables:

   Sometimes you need some environment variables (e.g: when cross-compiling a linux kernel):
   ```bash
   export CROSS_COMPILE=arm-linux-gnueabihf-
   export ARCH=arm
   ```
   > `CROSS_COMPILE` is used by many build systems to specify the cross-compilation toolchain prefix.
   > `ARCH` is used to set this to specify the architecture you're targeting.

5. Verify the toolchain:

   To confirm that the toolchain is installed and accessible, try checking the
   version of the ARM GCC compiler:
   ```bash
   arm-linux-gnueabihf-gcc --version
   ```
   If the setup is successful, you should see the version of arm-linux-gnueabihf-gcc.
   You can also verify other tools like the assembler (as) or linker (ld):

   ```bash
   arm-linux-gnueabihf-as --version
   arm-linux-gnueabihf-ld --version
   ```

6. Using the Toolchain

   Now your ARM toolchain should be set up correctly, and you can use it to
   cross-compile for ARM architectures. For example, to compile a C program, run:
   ```bash
   arm-linux-gnueabihf-gcc -o my_program my_program.c
   ```
