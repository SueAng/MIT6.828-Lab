# 2 Computer Organization 
## 2.1 Memory  
The basic unit of  memory is byte.  
8086  
four 16bit general purpose registers:AX BX CX DX,can be decomposed into two 8bit registers  
two 16bit index registers:SI DI ,can not be decomposed into two 8bit registers
two 16bit stack registers:SP BP
four 16bit segment registers:CS DS SS ES
one instruction register:IP
one FLAGS register:FLAGS,stores the important information about the result of a prevous instruction  
### Netwide Assembler  (NASM)
instruction operands:register,memory,immediate,implied
### Basic instructions
`mov` It moves data from one location to another  
    mov dest,src  
The data specified by src is copied to dest,both operands may not be memory operands  

    mov eax, 3 ; store 3 into EAX register(3 is a immediate operands)  
    mov bx, ax ; stroe the value of AX into BX register  
The ADD


    add eax, 4   ; eax = eax + 4 
    add al, ah   ; al = al + ah  
The SUB  

    sub bx, 4    ; bx = bx - 4  
    sub ebx, edi ; ebx = ebx - edi
The INC and DEC  

    inc   ecx    ; ecx++
    dec   dl     ; dl--  
### Directives  
generally used to either instruct the assembler to do something or inform the assembler of something  
* define constants
* define memory to store data into 
* group memory into segments
* conditionally include source code
* include other files
NASM code has many of the same preprocessor as C,and the preprocessor directives start with a % instead of a `# `as in C  
### The equ direactive
    symbol equ value 
define a constant used in assembly programe  
### The %define direactive 
define constant macros just as C,like `#define`  

    %define SIZE 100
       mov eax, SIZE  
























  