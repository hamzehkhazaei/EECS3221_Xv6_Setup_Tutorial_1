# Setting up Xv6 Operating System

## 🧠 What is Xv6?
[Xv6](https://pdos.csail.mit.edu/6.828/2019/xv6.html) is MIT's modern re-implementation of Dennis Ritchie's and Ken Thompson's **Unix Version 6 (V6)** released by Bell Labs in 1975, for educational purposes. It provides a compact and clean operating system that runs on both **x86 and RISC-V** architectures and is written entirely in **ANSI C**, with a small amount of assembly code. As MIT has stopped supporting the x86 architecture, in this course we will adopt the **xv6-riscv** version. Xv6 is designed not for production use, but to help students understand the **core concepts** of operating systems by studying and modifying real, working code. Its simplicity and well-structured codebase make it an ideal platform for learning how modern OS components are built and how they interact.


## 💡 Why Xv6?
- **Minimal and Understandable**: Unlike modern operating systems with millions of lines of code, Xv6 has **under 10,000 lines**, making it manageable for students to read and modify.
- **Unix-Based**: It preserves the elegant and time-tested design of Unix, including processes, system calls, file systems, and shell interaction.
- **Educational Design**: MIT has tailored Xv6 to align with teaching goals, focusing on clarity over performance or security.

## 📘 Learning Outcomes
By doing your projects on Xv6, you will:
- Gain hands-on experience with low-level systems programming.
- Understand how operating system abstractions are implemented.
- Develop the ability to debug kernel-level code.
- Be better prepared for working with or designing real operating systems.

## 🚀 Compiling and Running Xv6
Xv6 is a real operating system kernel, so it requires real hardware to boot. Fortunately, today we can emulate hardware in software. Programs like [QEMU](https://www.qemu.org) can emulate the functionality of a real physical CPU in software. i.e., QEMU implements the standard CPU loop: it fetches an instruction pointed to by the instruction pointer register (EIP), decodes it, performs all permission and condition checks, computes the outcome, increments EIP, and continues to the next instruction. In a nutshell, QEMU (Quick EMUlator) is a generic and open-source machine emulator and virtualizer. It can emulate hardware to run operating systems or programs for one architecture on a different architecture, or it can use hardware acceleration to virtualize efficiently. In this course, we will use QEMU as an emulator and not a hypervisor. 

Like a real PC platform, QEMU emulates the hardware boot protocol. QEMU starts by loading the disk sector at number 0 into memory location 0x7c00 and then jumping to it. Xv6 takes it from there. At a high level, for Xv6, it does not matter if it runs on the real hardware or under QEMU. Of course, emulation is slower than real hardware. Still, aside from that, as long as QEMU implements the CPU's logic correctly, we do not observe any deviations from real bare-metal execution. Surprisingly, QEMU is reasonably fast, so you, as a human, barely notice the difference.

Thanks to Jason Keltz (our EECS Computer Development Manager), all EECS servers are now running [QEMU](https://www.qemu.org) and toolchains for [RISC-V](https://en.wikipedia.org/wiki/RISC-V). So now you only need to log in to your account on any EECS server and run the following to compile and boot up Xv6:
```
$ git clone https://github.com/hamzehkhazaei/xv6-riscv
$ cd xv6-riscv
$ make qemu
```
Afterwards, you should see something like this:
```
...
xv6 kernel is booting

init: starting sh
$
```
Use the `ls` command to see the user programs on `xv6`. Try to run at least one of them. 

To terminate Xv6 and exit the emulator, press `Ctrl+a`, release, and then press `x`.
You are now finished with the Xv6 setup and may go ahead with your project.

## 🚀 Running Xv6 in Debug Mode
Sometimes we need to bring up Xv6 in debug mode so that we can trace the execution line by line to find the root cause of an error or for other purposes.
To do so, first start Xv6 in debug mode:
```
$ make
$ make qemu-gdb
```
Now open another terminal, or another tab, in the same folder of your Xv6 source code, i.e., `xv6-riscv` and run:
```
$ riscv64-unknown-elf-gdb -q -iex "set auto-load safe-path ."
```
Use `break <address>` to set a breakpoint and type `continue` to run until the breakpoint.

**Note:** For MacOS users, if `gdb-multiarch` doesn't exist, try `riscv64-unknown-elf-gdb`. If no gdb exists on your Mac, run:
```
$ brew install riscv64-elf-gdb
```


*Instructor: Hamzeh Khazaei*
