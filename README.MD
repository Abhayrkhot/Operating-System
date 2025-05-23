# LensorOS

**LensorOS** is a 64-bit, from-scratch operating system designed to provide a fully self-contained OS development environment. It includes a UEFI bootloader, a custom kernel, user-space utilities, memory management, ELF loading, and a standard library implementation. LensorOS aims to be educational, hackable, and modular, enabling developers to explore all aspects of low-level systems programming.

---

## Overview

- **Architecture:** x86_64
- **Boot Mode:** UEFI (via gnu-efi)
- **Kernel:** Monolithic, written in C and Assembly
- **Userspace:** Custom shell and utilities
- **Toolchain:** Custom GCC cross-compiler
- **Virtualization:** QEMU, VirtualBox, VMWare
- **Build System:** CMake-based

---

## Directory Structure

```
lensoros/
├── base/            # Core headers and shared components
├── kernel/          # LensorOS kernel source code
├── user/            # User-space programs and shell
├── std/             # Custom libc-like implementation
├── scripts/         # Utilities for build/run
├── toolchain/       # GCC cross-compilation toolchain
├── gnu-efi/         # UEFI bootloader using gnu-efi
├── OVMFbin/         # OVMF firmware binaries for QEMU
├── CMakeLists.txt   # Top-level CMake build file
├── README.md        # Project documentation
├── LICENSE          # GNU GPL v3 license
```

---

## Features

### Bootloader

- UEFI bootloader using `gnu-efi`
- Loads kernel in `ELF64` format
- Initializes framebuffer for graphical output
- Exposes memory map and ACPI tables to the kernel

### Kernel

- Pure 64-bit C kernel with minimal assembly
- Physical and virtual memory management (paging)
- ELF executable loading
- Process scheduler with multitasking support
- Interrupt Descriptor Table (IDT) and exception handling
- Basic device abstraction and input

### User Space

- Custom shell environment
- System calls for interacting with kernel
- Examples: echo, cat, ls, shutdown

### Development Toolkit

- GCC cross-compiler (x86_64-elf)
- CMake build system with modular project structure
- Run-ready QEMU scripts
- Debugging support via GDB

---

## Building the OS

### Requirements

Install the following packages:

- `nasm`, `cmake`, `make`, `gcc`, `binutils`
- `qemu-system-x86_64`
- `libgmp-dev`, `libmpfr-dev`, `libmpc-dev`
- `build-essential`, `bison`, `flex`
- `mtools`, `xorriso`

### 1. Build the Cross-Compiler Toolchain

```bash
cd toolchain
./build-toolchain.sh
```

### 2. Configure and Build LensorOS

```bash
mkdir build
cd build
cmake ..
make
```

---

## Running LensorOS

### Run with QEMU (Recommended)

```bash
./scripts/run-qemu.sh
```

This will launch QEMU with UEFI firmware (OVMF) and boot the OS image.

### Run on VirtualBox or VMWare

Use the ISO or IMG output found in the `build` directory. Ensure UEFI support is enabled.

---

## Debugging LensorOS

To debug using GDB:

```bash
./scripts/debug-qemu.sh
# In another terminal
gdb
(gdb) target remote localhost:1234
(gdb) symbol-file build/kernel/lensoros.elf
```

Ensure you enable the `-s -S` flags in your QEMU command.

---

## Project Goals

- Provide an educational platform for OS development
- Serve as a minimal but complete base for systems programming
- Encourage contribution to low-level software experimentation
- Support extensible userland with basic POSIX-like interfaces

---

## Roadmap

- [ ] Add file system support (FAT32 or ext2)
- [ ] Implement IPC (pipes, message queues)
- [ ] Extend virtual memory management
- [ ] Improve userspace ELF loader and shell
- [ ] Integrate basic GUI (framebuffer graphics)
- [ ] Enable SMP (multi-core processor support)

See `TODO.org` and `known_bugs.org` for more details.

---

