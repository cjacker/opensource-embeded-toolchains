# Embeded Toolchains in opensource way

This project aims to provide a series of step by step tutorials and related resources/tools/project templates to setup **opensource toolchains** and development environment **under Linux** for various **embeded devices**. 

It will include but not limited to 8051/avr/msp43x/stm8/stm32/riscv/fpga etc. 

These tutorials are not aim to teach beginners how to write codes for specific MCU. Although some project templates or examples to demo how to use a toolchain will be provided.

The goal of this project is **to help beginners setup a workable opensource toolchain and development environment to start MCU development quickly under Linux**, and to show what opensource community have done and the power of opensource software.

## What's a toolchain

A 'toolchain' generally means a set of programming tools include assembler/compiler/linker and debugger etc. for example, PC linux distributions provide 'binutils' as assembler/linker and various binary related tools, gcc/clang as compilers, gdb/lldb as debugger. the 'C compiler' pre-process source files and translate it to asm, the assembler 'gas' translate asm sources to target objects, and the linker 'ld/gold/lld' link various objects together and generate the final ELF binary. (by the way, Clang/LLVM is a little bit different, since it supports IR format)

Actually, you can always treat "compiler" as "translator", but a more complex "translator", and treat 'binary' such as ELF as a common 'file format'. since it's a 'file format' follow some rules, it can be generated any way even by hand.

You may need some project management tools to help you organize and build source files instead of typing compilation commands every time, there are make/automake/autoconf/ninja/cmake/scons/meson, etc.

You may also need an text editor to write codes, there are vim/emacs/vscode, etc.

That's to say, in narrow sense，'toolchain' is compiler. generally, a 'toolchain' should include all tools you need to do the software development. For embeded devices, beside compilers/debuggers, it should also include a flashing/programming tool to help you 'transfer' the softwares to target devices' flash or RAM, we usually call the software as 'firmware' or 'image', and call this 'transfer' process as 'flash' or 'program' or 'burn' or 'download/upload', etc. 

## What's a cross-compile toolchain

Usually, we work with a Intel or AMD PC/Laptop and with Linux installed, the toolchain described above runs on X86_64 architechture and generates binaries for X86_64 architechture. for example, linux OS can build itself on the same Linux OS and gcc/clang can build itself by gcc/clang. we call this as '**bootstrap**', here it means building itself by itself.

But we may also need to run toolchains on X86 PC and generate binaries for another architechture, such as ARM, AARCH64, MIPS, RISC-V, etc. Such a toolchain called '**cross-compile**' toolchain. you may already use it before, for example, NDK toolchain of Android or IOS toolchain, it runs on X86 PC host but generates binaries for ARM target.

You may notice the commands of such a 'cross-compile' toolchain always start with a special string, such as 'arm-none-eabi-gcc', and may also find such a string if you run 'gcc -v' on PC linux, for example, "x86_64-redhat-linux". such a string called **['triplet'](https://wiki.osdev.org/Target_Triplet)**, toolchain's triplet have this simple structure: 

```
machine-vendor-operatingsystem
```

The 'machine' field usually indicates the 'architechture', such as x86_64, arm, aarch64, riscv, etc. the 'vendor' field usually contains the brand of vendor, and the 'operatingsystem' usually is the os name, the c library name or abi name.

For instance:
* 'x86_64-unknown-linux[-gnu]' means target is x86_64 machine / unknown vendor / linux OS with glibc, sometime '-gnu' may be omitted.
* 'x86_64-alpine-linux-musl' means target is x86_64 machine / alpine linux / linux OS with musl libc.
* 'arm-none-eabi' means target is arm machine / not limited to specific vendor / without requiring of os and with embedded-application binary interface(EABI) support.

Besides above rules, toolchian's triplet is used by compilers to find corresponding assemblers/linkers with the same triplet. for example, 'arm-none-eabi-gcc' usually use 'arm-none-eabi-as' as its assembler, it's not mandary but a convention in toolchain's source codes.

For a 'cross-compile' toolchain with OS support, there is also need a target os '**sysroot**' which contains the root filesystem and libraries of the target system that the compiler can find headers and link to target libs.

For embeded device, most MCU do **NOT** require a seperate OS installed, we call it 'baremetal'.

## Why should I use opensource toolchain

No, you do not have to, but why not.

Actually, opensource toolchains already rule the world and you may already use them before such as clang/gcc/gdb and openocd.

## Toolchain Tutorials

Every tutorial and related resources will be provided in a seperate repo:

**For any issues, welcome to submit issue or pull request to corresponding repo.**

- [8051](https://github.com/cjacker/opensource-toolchain-8051) (mainly for STC51 series) **[DONE]**
- [STM8](https://github.com/cjacker/opensource-toolchain-stm8) **[DONE]**
- AVR
- [MSP430](https://github.com/cjacker/opensource-toolchain-msp430) **[DONE]**
- STM32
- [GD32VF103 (RISC-V 32bit MCU based on nuclei core)](https://github.com/cjacker/opensource-toolchain-gd32vf103) **[DONE]**
- [WCH CH32V series RISC-V 32bit MCU](https://github.com/cjacker/opensource-toolchain-ch32v) **[DONE]**
- [RPI Pico RP2040](https://github.com/cjacker/opensource-toolchain-rp2040) **[DONE]**
- [Lattice ECP5/ICE40 FPGA](https://github.com/cjacker/opensource-toolchain-fpga) **[DONE]**
- [Gowin LittleBee FPGA](https://github.com/cjacker/opensource-toolchain-fpga) **[DONE]**

- Allwinner D1 nezha(not MCU)
  - PhoenixCard (the SD card image flashing tool) is not opensource and only for Windows, seems without image format specification.

**Which will not have a tutorial:**

- PIC16/18
  - the whole product line is not opensource friendly.
  - you need special and expensive programmer, only PICkit2 has opensource flash tool support (pk2cmd) and it does not support all models.
  - There is MPLAB X IDE for linux and xc8 with free license, if you do not care about opensource or not. 

- ~~WCH CH32V series RISC-V 32bit MCU~~
  - It does NOT support standard debugging interface such as SWD/JTAG
  - It implemented a private protocol named RVSWD and modified OpenOCD codes, ~~but not opensourced.~~ **2022-05-22, recently WCH opened forked OpenOCD source codes, I will write a tutorial for it.**
  - ~~**Please resist using such product until it follows LICENSE and opensource the codes.**~~

