# arm-linux-gnu

The **arm-linux-gnu toolchain** is a set of tools used to build software for ARM-based systems running Linux. It includes compilers, linkers, assemblers, and other utilities, all designed to target ARM architectures. When discussing **EABI-0** or **noeabi**, we are referring to specific ABI (Application Binary Interface) conventions used in the ARM architecture, which dictates how functions are called, how data is passed between functions, and how data is laid out in memory. Let’s break down the concepts:

## Toolchain

### 1. **Toolchain Overview:**
The **arm-linux-gnu toolchain** typically consists of:
- **GCC** (GNU Compiler Collection) for compiling code
- **Binutils** for binary utilities like assembler, linker, and object file manipulation
- **Newlib** or other C libraries (depending on the ABI)

This toolchain produces code that runs on ARM processors with a Linux operating system.

### 2. **EABI (Embedded Application Binary Interface):**
**EABI** is an ABI specification for ARM architectures, originally designed for embedded systems, and it specifies how the ARM architecture should interact with software at the binary level. There are various versions of EABI depending on the specifics of the system, like whether or not it supports hardware floating-point, the calling conventions, or data alignment.

#### **EABI-0** vs **EABI (noeabi):**
- **EABI-0** is an early version of the EABI standard for ARM processors. It specifies how functions should be called, how arguments should be passed, and how return values are handled.
- **noeabi** (or **"No EABI"**) refers to using a toolchain that does **not** conform to the full EABI specification. When building with **noeabi**, the toolchain ignores EABI conventions and may use a simpler or more legacy ABI, such as the "old ABI" used by earlier versions of ARM systems. This may be used in situations where full EABI support isn't necessary or desirable, for instance, when targeting older ARM processors or very constrained environments.

### 3. **Key Differences between EABI and NoEABI:**

- **EABI**: Adheres to ARM’s Embedded Application Binary Interface specifications, including things like calling conventions, argument passing, and system call conventions. This is the more modern, standardized ABI used by most contemporary ARM Linux systems.
  
  - Supports hardware floating point (if available).
  - Standardized function calling conventions.
  - Better compatibility with standard libraries (like `glibc`).
  
- **NoEABI (No EABI)**: Does not adhere to these conventions, using either a custom or legacy ABI instead. This may be used for minimal systems, specialized environments, or old systems where compatibility with EABI is unnecessary.
  
  - May lack floating point support or use software floating point.
  - Could have non-standard calling conventions and memory layout.
  - Used for more constrained, low-level, or older embedded systems.
  
### 4. **EABI and NoEABI Usage Scenarios:**
- **EABI** is most commonly used when building applications for modern ARM Linux systems. If you are targeting recent Linux distributions running on ARM, this is the ABI you’d typically use.
- **NoEABI** is generally reserved for legacy systems, where the newer ABI might introduce compatibility issues or isn't needed. It may also be used in certain bare-metal environments or systems with very limited resources.

### 5. **Building for EABI or NoEABI:**
The way to select **EABI-0** or **noeabi** in the ARM toolchain is usually done by specifying the correct target triplet when invoking the toolchain's GCC or other build tools. The target triplet defines the architecture and ABI, and it typically looks something like `arm-linux-gnueabi` or `arm-linux-gnueabihf` (for hard float support).

For example:
- For **EABI**: `arm-linux-gnueabi-gcc` or `arm-linux-gnueabihf-gcc` (if you're using hard-float).
- For **NoEABI**: The triplet might be something like `arm-linux-gnu-gcc`, which suggests no EABI support.

### 6. **Toolchain Configuration:**
The configuration and version of the toolchain can have a significant impact on whether you are building with EABI or NoEABI. The toolchain’s configuration flags or environment variables might allow you to explicitly specify which ABI to use.

For example:
- `--with-abi=soft` (software floating-point) or `--with-abi=hard` (hardware floating-point) can affect the ABI chosen during compilation.
- `--with-fpu` or `--with-float` may configure floating-point behavior if you are using EABI, while in NoEABI, you may not have hardware floating-point support.

### Summary:
- **arm-linux-gnu** toolchain is used to build software for ARM Linux systems.
- **EABI** is a standard ABI for ARM, defining function calling conventions, argument passing, and data alignment.
- **EABI-0** is an earlier version of the EABI.
- **NoEABI** refers to using a non-standard or legacy ABI, possibly for very constrained systems or older ARM platforms.
- The **arm-linux-gnu toolchain** can be used with either EABI or NoEABI, depending on the target system's requirements.

If you're working with ARM-based embedded Linux systems and want compatibility with modern libraries, EABI (and its versions like EABI-0) is the way to go. NoEABI may be used for very specialized or legacy systems, but it comes with some trade-offs in terms of compatibility with modern development tools and libraries.



## Ports Dependency tree

```
 gcc-arm-linux-gnu (4.7.4)
   glibc-arm-linux-gnu (2.11.3)
     static-gcc-arm-linux-gnu (4.7.4)
       binutils-arm-linux-gnu (2.23.2)
         libmpc-arm-linux-gnu (1.3.1)
           libmpfr-arm-linux-gnu (4.2.1)
             libgmp-arm-linux-gnu (6.3.0)
               kernel-headers-arm-linux-gnu (3.16.85)
       kernel-headers-arm-linux-gnu (3.16.85)
     make43 (4.3)
     kernel-headers-arm-linux-gnu (3.16.85)
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

