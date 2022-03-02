# Opensource Embeded Toolchains under Linux

This project aims to provide a series of step by step tutorials and related resources/tools/project templates to setup **opensource toolchains** and development environment **under Linux** for various common **embeded devices**. 

It will include but not limited to 8051/avr/stm8/stm32/riscv/fpga etc. 

These tutorials are not aim to teach beginners how to write codes for specific MCU. although some project templates or examples to demo how to run a toolchain will be provided, but it's not the first goal.

The first goal of this project is **to help beginners setup a workable toolchain and development environment to start MCU development quickly under Linux**, and to show the power of opensource software and what opensource community have done.

## What's a toolchain

A 'toolchain' gennerally means a set of programming tools include assembler/compiler/linker and debugger etc. for example, PC linux distributions provide 'binutils' as assembler/linker and various binary related tools, gcc/clang as compilers, gdb/lldb as debugger. the 'C compiler' pre-process source files and translate it to asm and the assembler 'gas' translate asm sources to target objects, and the linker 'ld/gold/lld' link various objects together and generate the final ELF binary, maybe it's a excutable binary or a library. (by the way, Clang/LLVM is a little bit difference, since it supports IR format)

Acctually, you can always treat "compiler" as "translator", but a more complex "translator", and treat 'binary' such as ELF as a 'file format'. since it's a 'file format' with some rules, it can be generated any way even by hand.

You may need project managing tools to help you organize and build source files instead of typing compilation commands every time, there are make/automake/autoconf/ninja/cmake/scons/meson, etc.

You may also need an editor to write codes, there are vim/emacs/vscode, etc.

That's to say, in narrow sense，'toolchain' is compiler and debugger. generally, a 'toolchain' should include all tools you need to do the software development. 

For embeded devices, beside compilers/debuggers, it should also include a flashing/programming tool to help you 'transfer' the softwares to target devices' storage or RAM, we usually call the software as 'firmware' or 'image', and call this 'transfer' process as 'flash' or 'program' or 'burn' or 'download', etc. 

## What's a cross-compile toolchain

Usually, we work with a Intel or AMD PC/Laptop and with Linux installed, the toolchain described above run on X86_64 architechture and generate binaries for X86_64 architechture. for example, linux OS can build itself on the same Linux OS and gcc/clang can build itself by gcc/clang. we call this '**bootstrap**', here it means building itself by itself.

But we may also need to run toolchains on X86 PC and generate binaries for another architechture, such as ARM, AARCH64, MIPS, RISC-V, etc. Such a toolchain called '**cross-compile**' toolchain. you may already use it before, for example, NDK toolchain of Android or IOS toolchain, it run on X86 PC host but generate binaries for ARM target.

You may notice that commands of such a 'cross-compile' toolchain always start with a special string, such as 'arm-none-eabi-gcc', and may also find such a string if you run 'gcc -v' on your PC linux, for example, "x86_64-redhat-linux". such a string called **['triplet'](https://wiki.osdev.org/Target_Triplet)**, toolchain's triplet have this simple structure: 

```
machine-vendor-operatingsystem
```

The 'machine' field usually indicate the 'architechture', such as x86_64, arm, aarch64, riscv, etc. the 'vendor' field usually contains the brand of vendor, and the 'operatingsystem' usually contains the os name, the c library name or abi name.

For instance:
* 'x86_64-unknown-linux[-gnu]' means target is x86_64 machine / unknown vendor / linux OS with glibc, sometime '-gnu' may be omitted.
* 'x86_64-alpine-linux-musl' means target is x86_64 machine / alpine linux / linux OS with musl libc.
* 'arm-none-eabi' means target is arm machine / not limited to specific vendor / without requiring of a os and with embedded-application binary interface(EABI) support.

Besides above rules, toolchian's triplet is used by compilers to find corresponding assemblers/linkers with same triplet. for example, 'arm-none-eabi-gcc' usually use 'arm-none-eabi-as' as its assembler, it's not mandary but a convention in toolchain's source codes.

For a 'cross-compile' toolchain with OS support, there is also need a target os '**sysroot**' which contains the root filesystem and libraries of target system that the compiler can find headers and link to target libs.

For embeded device, most MCU do **NOT** require a seperate OS installed, we call it 'baremetal'.

## Why should I use opensource toolchain

No, you do not have to, but why not.

Actually, opensource toolchain already rule the world and you may already use it before.

## Toolchain Tutorials

This project will include but not limited to below tutorials, every tutorial and related resources will be provided by a seperate repo:

**For any updates/mistakes/troubles/issues/improvements, etc., welcome to submit issues or pull request to corresponding repo.**


- [8051](https://github.com/cjacker/opensource-toolchain-8051)(mainly for STC51 series) **[DONE]**
- [STM8](https://github.com/cjacker/opensource-toolchain-stm8) **[DONE]**
- [GD32VF103(RISC-V 32bit MCU based on nuclei core)](https://github.com/cjacker/opensource-toolchain-gd32vf103) **[DONE]**
- AVR
- STM32
- RPI Pico RP2040
- Lattice FPGA ECP5/ICE40 **[DOING]**
- Gowin FPGA littlebee **[DOING]**
- PIC?
- MSP430?
- CH32V(RISC-V 32bit MCU)
  - It does NOT support standard debugging interface such as SWD/JTAG
  - It implemented a private protocol named RVSWD and modified OpenOCD codes, but not opensourced.
  - **Please resist using such product until it follows the requirements of LICENSE and opensource their codes.**
- Allwinner D1 nezha(not MCU)
  - PhoenixCard (the SD card image burning tool) is not opensource and only for Windows.

This series of tutorials will not cover Raspberry Pi. it's a slow PC with IO PIN and has nothing special.
