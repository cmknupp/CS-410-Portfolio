### Just wanted to say thanks for posting this.  I was floundering with this assignment as I had to install GDB before any of the commands would work and I thought I was not doing it correctly.  Your github helped assure me I was
### on the right track.  I appreciate you.  Also helpful note:  x/s <hex address> will give you the string or formatting string at a given location. I added an example below. 

# Assignment 3.2

## Binary file to hex

[assignment3_2.o hex dump](assignment3_2_hex_dump.txt)

## GDB Commands

### Identify the functions in the binary file

```bash
(gdb) info functions
All defined functions:

Non-debugging symbols:
0x00000000004004a8  _init
0x00000000004004e0  puts@plt
0x00000000004004f0  printf@plt
0x0000000000400500  __libc_start_main@plt
0x0000000000400510  __gmon_start__@plt
0x0000000000400520  __isoc99_scanf@plt
0x0000000000400530  exit@plt
0x0000000000400540  _start
0x0000000000400570  deregister_tm_clones
0x00000000004005a0  register_tm_clones
0x00000000004005e0  __do_global_dtors_aux
0x0000000000400600  frame_dummy
0x000000000040062d  main
0x0000000000400690  __libc_csu_init
0x0000000000400700  __libc_csu_fini
0x0000000000400704  _fini
```

### Assembly code for the main function

```bash
(gdb) disassemble main
Dump of assembler code for function main:
   0x000000000040062d <+0>:     push   %rbp
   0x000000000040062e <+1>:     mov    %rsp,%rbp
   0x0000000000400631 <+4>:     sub    $0x20,%rsp
   0x0000000000400635 <+8>:     mov    %fs:0x28,%rax
   0x000000000040063e <+17>:    mov    %rax,-0x8(%rbp)
   0x0000000000400642 <+21>:    xor    %eax,%eax
   0x0000000000400644 <+23>:    mov    $0x400714,%edi
   0x0000000000400649 <+28>:    callq  0x4004e0 <puts@plt>
   0x000000000040064e <+33>:    lea    -0x20(%rbp),%rax
   0x0000000000400652 <+37>:    mov    %rax,%rsi
   0x0000000000400655 <+40>:    mov    $0x40072b,%edi
   0x000000000040065a <+45>:    mov    $0x0,%eax
   0x000000000040065f <+50>:    callq  0x400520 <__isoc99_scanf@plt>
   0x0000000000400664 <+55>:    lea    -0x20(%rbp),%rax
   0x0000000000400668 <+59>:    mov    %rax,%rsi
   0x000000000040066b <+62>:    mov    $0x40072e,%edi
   0x0000000000400670 <+67>:    mov    $0x0,%eax
   0x0000000000400675 <+72>:    callq  0x4004f0 <printf@plt>
   0x000000000040067a <+77>:    mov    $0x0,%edi
   0x000000000040067f <+82>:    callq  0x400530 <exit@plt>
End of assembler dump.
```
### Determining strings example

```bash
(gbd) x/s 0x400714
0x400714:   "Please enter your name"
