# Opensource Embeded Toolchains under Linux

This project aims to provide a series of step by step tutorials and related resources/tools/project templates to setup **opensource toolchains** and development environment **under Linux** for various common **embeded devices**. 

It will include but not limited to 8051/avr/stm8/stm32/riscv/fpga etc. 

These tutorials are not aim to teach beginners how to write codes for specific MCU. although some project templates or examples to demo how to run a toolchain will be provided, but it's not the first goal.

The first goal of this project is to help beginners setup a workable toolchain and development environment to start MCU development quickly under Linux, and to show the power of opensource software and what opensource community can do .

## What's a toolchain

A 'toolchain' gennerally means a set of programming tools include assembler/compiler/linker and debugger etc. for example, PC linux distributions provide 'binutils' as assembler/linker and various binary related tools, gcc/clang as compilers, gdb/lldb as debugger. the 'C compiler' pre-process source files and translate it to asm and the assembler 'gas' translate asm sources to target objects, and the linker 'ld/gold/lld' link various objects together and generate the final ELF binary, maybe it's a excutable binary or a library. Acctually, you can always treat "compiler" as "translator", but it's a more complex "translator". (by the way, Clang/LLVM is a little bit difference, since it supports IR format)

You may need project managing tools to help you organize and build source files instead of typing compilation commands every time, there are make/automake/autoconf/ninja/cmake/scons/meson, etc.

You may also need an editor to write codes, there are vim/emacs/vscode, etc.

That's to say, in narrow sense，'toolchain' is compiler and debugger. generally, a 'toolchain' should include all tools you need to do the software development. 

For embeded devices, beside compilers/debuggers, it should also include a flashing/programming tool to help you 'transfer' the softwares to target devices, we usually call such software for embeded device as 'firmware', it may have or have not an operating system. by the way, we call it 'baremetal' if without a OS. 

## Toolchain Tutorials

This project will include but not limited to below tutorials, every tutorial and related resources will be provided by a seperate repo:

- [8051](https://github.com/cjacker/opensource-toolchain-8051)(mainly for STC51 series)
- [STM8](https://github.com/cjacker/opensource-toolchain-stm8)
- PIC?
- MSP430?
- AVR
  - low priority since Arduino has a great development platform for Linux.
- STM32
- [GD32VF103(RISC-V 32bit MCU based on nuclei core)](https://github.com/cjacker/opensource-toolchain-gd32vf103)
- CH32V(RISC-V 32bit MCU based on nuclei core)
  - I still consider write a tutorial for it or not. since its vendor use modified OpenOCD to support private protocol RVSWD but not opensourced, we should resist using such product.
- RaspberryPi PICO RP2040
- Lattice FPGA ECP5/ICE40
- Gowin FPGA littlebee
- Allwinner D1 nezha(not MCU)
  - PhoenixCard (the SD card image burning tool) is not opensource and only for Windows.
