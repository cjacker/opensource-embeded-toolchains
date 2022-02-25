# Opensource Embeded Toolchains under Linux
This project aims to provide a step by step tutorial and related resources to setup **opensource toolchains** and development environment **under Linux** for various common **embeded devices**. 

It will include but not limited to 8051/avr/stm8/stm32/riscv/fpga etc.

## what's a toolchain
A 'toolchain' gennerally means a set of programming tools include assembler/compiler/linker and debugger etc. for example, a lot of PC linux distributions provide 'binutils' as assembler/linker and various binary related tools, gcc/clang as compilers, gdb/lldb as debugger. the 'C compiler' pre-process source files and translate it to asm source file and the assembler 'gas' translate asm source file to target object, and the linker 'ld/gold/lld' link various objects and form the final ELF binary, maybe a excutable binary or a library. acctually, "compiler" is a "translator", but a complex "translator". by the way, Clang/LLVM is a little bit difference, since it supports IR format.

You may also need project managing tools to manage how to organize and build source files instead of typing compilation command every time, there are make/automake/autoconf/ninja/cmake/scons/meson, etc.

You may need an editor to write codes, there are vim/emacs/vscode/kak, etc.

That's to say, in narrow sense， 'toolchain' is compiler and debugger, but not limited to it, a 'toolchain' should include all tools you need to finish the software development. 

For embeded devices, beside compilers/debuggers, it should also include a flash tool to help you deploy softwares to target devices.

## 8051
A lot of vendors provide 8051 MCU, such as Atmel AT89/90 series, STC stc89/90/10/11/12/15/8x series and WCH ch5xx series. 

8051 MCU is very old and the development is very simple, a lot of people complain that 'the resource of 8051 is very limited'. 

Yes, it's. but for a beginner, maybe 8051 is the best choice to start learning embede development. since it have everything you need to know about embeded device development and **IT IS SIMPLE**.

This tutorial is focus on STC 8051 MCU.

### compiler


