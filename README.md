# Embeded Toolchains in opensource way

**NOTE: the MIT license of this repo means all individual resources made by myself, the content of the tutorial and the example codes is licensed under MIT. All third-party opensource projects, upstream source codes and patches to other opensource projects will/should follow their own LICENSE.**

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

For embeded device, most MCU do **NOT** require a seperate OS installed, we call it 'baremetal', it means without requirement to have a OS.

## Is there any good opensource debug solution for specific MCU?

Any toolchain based on GNU opensource toolchain should have complete opensource debug solution based on gdb/OpenOCD.

Some 8-bit MCUs does not use GNU toolchain, most of them were supported by SDCC, and maybe lack of opensource debug support.

But you should understand that MCU software/firmware development is different with common PC software development.

Debugging MCU code isn't quite the same as debugging code for a PC because the MCU code is usually controlling physical outputs or receiving physical inputs to/from the real world and the debugging process has to take those into account. Since the signal sequences to communicate with peripheral devices is time-critical, you can not break or pause it as PC software development, the software debugger won't help you too much. 

Usually the MCU debugging process is always combined with simulator, debugger, Serial print and logic analyzer etc.

Thus, 'lack of opensource debug sulotion with specific MCU' is not a big issue to using the opensource toolchain in real project.

## Why should I use opensource toolchain?

No, you do not have to, but why not.

Actually, opensource toolchains already rule the world and you may already use them before such as clang/gcc/gdb and openocd.

## Toolchain Tutorials

Every tutorial and related resources will be provided in a seperate repo:

**For any issues, welcome to submit issue or pull request to corresponding repo.**

**8 bit**

- [8051](https://github.com/cjacker/opensource-toolchain-8051) **[DONE]**
- [STM8](https://github.com/cjacker/opensource-toolchain-stm8) **[DONE]**
- [AVR](https://github.com/cjacker/opensource-toolchain-avr) **[DONE]**
- [PIC](https://github.com/cjacker/opensource-toolchain-pic) **[DONE]**
- Padauk

**16 bit**

- [MSP430](https://github.com/cjacker/opensource-toolchain-msp430) **[DONE]**

**32 bit**

- STM32 (ARM)
- [GD32VF103 (RISC-V 32bit MCU based on nuclei core)](https://github.com/cjacker/opensource-toolchain-gd32vf103) **[DONE]**
- [WCH CH32V (RISC-V 32bit MCU)](https://github.com/cjacker/opensource-toolchain-ch32v) **[DONE]**
- [RPI Pico RP2040 (ARM)](https://github.com/cjacker/opensource-toolchain-rp2040) **[DONE]**

**64 bit**

- Allwinner D1 nezha(not MCU)
  - PhoenixCard (the SD card image flashing tool) is not opensource and only for Windows, seems without image format specification.

**fpga**

- [Lattice ECP5/ICE40 FPGA](https://github.com/cjacker/opensource-toolchain-fpga) **[DONE]**
- [Gowin LittleBee FPGA](https://github.com/cjacker/opensource-toolchain-fpga) **[DONE]**


**Which will not have a tutorial:**

- ~~8bit PIC~~
  - ~~gputils and~~the PIC part of SDCC is un-maintained now. **gputils updated recently and there is gcbasic and jal for PIC with very active development.**
  - There is official MPLAB X IDE for linux and xc8 with free license, if you do not care about opensource or not. but xc8 has worse optimizations with free license.
  
- ~~WCH CH32V series RISC-V 32bit MCU~~
  - It does NOT support standard debugging interface such as SWD/JTAG
  - It implemented a private protocol named RVSWD and modified OpenOCD codes, ~~but not opensourced.~~ **2022-05-22, recently WCH opened the source code of its' private forked OpenOCD, I will write a tutorial for it.**
  - ~~**Please resist using such product until it follows LICENSE and opensource the codes.**~~

