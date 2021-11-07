# OS
-----notes before you get started-----
1. in developing an operating system, you cannot and cannot and cannot use <iostream>, <fstream>, <memory>, <cstdio>, <cstdlib>, <windows.h>, <unistd.h> 
and all the platform API'syou must create all of them yourself
2. you must very very be careful
when you are developing, you have control of everything
so, you can destroy one or some or all of your hardwares
in this case, i recommend to use a virtual machine to test your operating system instead of rebooting more and more times

-----how to compile it-------
go to the shell (on windows cygwin is required):
type these commands:

nasm -f elf boot.asm -o boot.o
g++ -c kernel.cpp -o kernel.o -ffreestandinng -fno-exceptions -fno-rtti
gcc loader.o kernel.o -T linker.ld -o kern -nostdlib -nodefaultlibs -lgcc

kingratulations!
your first operating system has been compiled successfully!
now you can create an image using grub-mkrescue:
create a directory: iso
in that directory, create another directory: boot then in the boot directory, create a directory: grub and then create a file: grub.cfg with these contents(do not add the braces in a new line) in the grub directory:

menuentry "myOS" {
multiboot /boot/kern
}

then copy your kernel (kern) to iso/boot directory and run your shell again:
switch to the main directory of your kernel and type:
 
grub-mkrescue iso --output=kern.iso

now you can boot and enjoy from your first operating system:: this simple kernel without anything
