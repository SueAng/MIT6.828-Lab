# Lab1: Booting a PC
This lab split into three parts:  
* get familiaried with x86 assembly language, the QEMU x86 emulator, and the PC power-on bootstrap procedure.
* eaxmines the boot loader for 6.828 kernel
* delves into the initial template for our 6.828 kernel itself, named JOS  
## Part 1: PC Bootstrap
### Getting Started with x86 assembly
read [PC Assembly Language Book](https://pdos.csail.mit.edu/6.828/2018/reference.html), and [ Brennan's Guide to Inline Assembly](http://www.delorie.com/djgpp/doc/brennan/brennan_att_inline_djgpp.html).  
### Exercise1  
Familiarize yourself with the assembly language materials available on [the 6.828 reference page](https://pdos.csail.mit.edu/6.828/2018/reference.html). Read the section "The Syntax" in  [ Brennan's Guide to Inline Assembly](http://www.delorie.com/djgpp/doc/brennan/brennan_att_inline_djgpp.html)  
AT&T assembly syntax  
* register name: prefixed "%"  
     ```  
    AT&T: %eax     
    Intel: eax
     ```
* Source/Destination Ordering:  the source is always on the left, and the destination is always on the right  
     ```
    AT&T: movl %eax, %ebx
    Intel: mov ebx, eax  
     ```  
* Constant value/immediate value format: prefix all constant/immediate values with "$"  
     ```
     AT&T: movl $_booga, %eax
     Intel: mov eax, _booga

     AT&T: movl $0xd00d, %eax
     Intel: mov eax, d00dh
     ```  
* Operator size specifiction: suffix the instruction with one of b, w, or l to specify the destination register as a byte, word or longword  
     ```
     AT&T: movw %ax, %bx
     Intel: mov bx, ax
     ```
* Referencing memory
     ```
     AT&T: immed32(basepointer, indexscale)
     Intel: [baseponter+indexpointer*indexscale+immed32]
     ```
* Addressing a particular C variable:
     ```
     AT&T: _booga
     Intel: [_booga]
     ```
* Addressing what a register points to:
     ```
     AT&T: (%eax)
     Intel: [eax]
     ```
* Addresing a variable offset by a value in register:
     ```
     AT&T: _variable(%eax)
     Intel: [eax + _variable]
     ```
* Addressing a value in an array of integers(scaling up by 4):
     ```
     AT&T: _array(,%eax,4)
     Intel: [eax*4 + array]
     ```
* You can do offsets with the immediate value:
     ```
     C code: *(p+1) where p is a char *
     AT&T: 1(%eax) where eax has the value of p
     Intel: [eax+1]
     ```
* You can do some simple math on the immediate value:
     ```
     AT&T: _struct_pointer+8
     ```
* Addressing a particular char in an array of 8-character records:  
     ```
     AT&T: _array(%ebx,%eax,8)  
     Intel: [ebx + eax*8 + _array]