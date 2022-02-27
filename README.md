# Opensource Embeded Toolchains under Linux

This project aims to provide a series of step by step tutorials and related resources to setup **opensource toolchains** and development environment **under Linux** for various common **embeded devices**. 

It will include but not limited to 8051/avr/stm8/stm32/riscv/fpga etc.

## what's a toolchain
A 'toolchain' gennerally means a set of programming tools include assembler/compiler/linker and debugger etc. for example, a lot of PC linux distributions provide 'binutils' as assembler/linker and various binary related tools, gcc/clang as compilers, gdb/lldb as debugger. the 'C compiler' pre-process source files and translate it to asm and the assembler 'gas' translate asm sources to target objects, and the linker 'ld/gold/lld' link various objects and form the final ELF binary, maybe a excutable binary or a library. acctually, you can treat "compiler" as "translator", but a more complex "translator". (by the way, Clang/LLVM is a little bit difference, since it supports IR format)

You may need project managing tools to help you organize and build source files instead of typing compilation commands every time, there are make/automake/autoconf/ninja/cmake/scons/meson, etc.

You may also need an editor to write codes, there are vim/emacs/vscode, etc.

That's to say, in narrow sense，'toolchain' is compiler and debugger. Generally, a 'toolchain' should include all tools you need to do the software development. 

For embeded devices, beside compilers/debuggers, it should also include a flash tool to help you 'transfer' softwares to target devices.

## tutorials

this project will include but not limited to below tutorials.
- 8051(mainly STC51 series)
- ![STM8](https://github.com/cjacker/opensource-toolchain-stm8)
- PIC?
- MSP430?
- AVR
  - low priority since Arduino has a great and out-of-box development platform for Linux.
- STM32
- ![GD32VF103(RISC-V 32bit MCU based on nuclei core)](https://github.com/cjacker/opensource-toolchain-gd32vf103)
- CH32V(RISC-V 32bit MCU based on nuclei core)
  - I still consider write a tutorial for it or not. since its vendor use modified OpenOCD to support its private protocol RVSWD but not opensourced, maybe we should resist using such products.
- RaspberryPi PICO RP2040
- Lattice FPGA ECP5/ICE40
- Gowin FPGA littlebee
- Allwinner D1 nezha(not MCU)
  - PhoenixCard is not opensourced and only for Windows.
