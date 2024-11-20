## Objetivo
Now for something a little different. `0x2262c96b` is loaded into memory in the `main` function. Examine byte-wise the memory that the constant is loaded in by using the GDB command `x/4xb addr`. The flag is the four bytes as they are stored in memory. If you find the bytes `0x11 0x22 0x33 0x44` in the memory location, your flag would be: `picoCTF{0x11223344}`. Debug [this](https://artifacts.picoctf.net/c/531/debugger0_c).
## Solución

```bash
┌──(armando㉿kali)-[~/picoCTF/reversing/GDBbabystep3]
└─$ ls -la
total 24
drwxrwxr-x  2 armando armando  4096 Nov 16 18:01 .
drwxrwxr-x 22 armando armando  4096 Nov 16 18:01 ..
-rw-rw-r--  1 armando armando 16304 Aug  4  2023 debugger0_c

┌──(armando㉿kali)-[~/picoCTF/reversing/GDBbabystep3]
└─$ chmod +x debugger0_c

┌──(armando㉿kali)-[~/picoCTF/reversing/GDBbabystep3]
└─$ ls -la              
total 24
drwxrwxr-x  2 armando armando  4096 Nov 16 18:01 .
drwxrwxr-x 22 armando armando  4096 Nov 16 18:01 ..
-rwxrwxr-x  1 armando armando 16304 Aug  4  2023 debugger0_c

┌──(armando㉿kali)-[~/picoCTF/reversing/GDBbabystep3]
└─$ gdb debugger0_c 
GNU gdb (Debian 15.1-1) 15.1
Copyright (C) 2024 Free Software Foundation, Inc.
License GPLv3+: GNU GPL version 3 or later <http://gnu.org/licenses/gpl.html>
This is free software: you are free to change and redistribute it.
There is NO WARRANTY, to the extent permitted by law.
Type "show copying" and "show warranty" for details.
This GDB was configured as "x86_64-linux-gnu".
Type "show configuration" for configuration details.
For bug reporting instructions, please see:
<https://www.gnu.org/software/gdb/bugs/>.
Find the GDB manual and other documentation resources online at:
    <http://www.gnu.org/software/gdb/documentation/>.

For help, type "help".
Type "apropos word" to search for commands related to "word"...
Reading symbols from debugger0_c...
(No debugging symbols found in debugger0_c)
(gdb) set disassembly-flavor intel 
(gdb) info functions 
All defined functions:

Non-debugging symbols:
0x0000000000401000  _init
0x0000000000401020  _start
0x0000000000401050  _dl_relocate_static_pie
0x0000000000401060  deregister_tm_clones
0x0000000000401090  register_tm_clones
0x00000000004010d0  __do_global_dtors_aux
0x0000000000401100  frame_dummy
0x0000000000401106  main
0x0000000000401130  __libc_csu_init
0x00000000004011a0  __libc_csu_fini
0x00000000004011a8  _fini
(gdb) disassemble main 
Dump of assembler code for function main:
   0x0000000000401106 <+0>:     endbr64
   0x000000000040110a <+4>:     push   rbp
   0x000000000040110b <+5>:     mov    rbp,rsp
   0x000000000040110e <+8>:     mov    DWORD PTR [rbp-0x14],edi
   0x0000000000401111 <+11>:    mov    QWORD PTR [rbp-0x20],rsi
   0x0000000000401115 <+15>:    mov    DWORD PTR [rbp-0x4],0x2262c96b
   0x000000000040111c <+22>:    mov    eax,DWORD PTR [rbp-0x4]
   0x000000000040111f <+25>:    pop    rbp
   0x0000000000401120 <+26>:    ret
End of assembler dump.
```
- Creamos un `breakpoint` al principio del `main` para que se detenga la ejecución del programa.
```bash
(gdb) break main 
Breakpoint 1 at 0x40110e
(gdb) run 
Starting program: /home/armando/picoCTF/reversing/GDBbabystep3/debugger0_c 
[Thread debugging using libthread_db enabled]
Using host libthread_db library "/lib/x86_64-linux-gnu/libthread_db.so.1".

Breakpoint 1, 0x000000000040110e in main ()
(gdb) disassemble main 
Dump of assembler code for function main:
   0x0000000000401106 <+0>:     endbr64
   0x000000000040110a <+4>:     push   rbp
   0x000000000040110b <+5>:     mov    rbp,rsp
=> 0x000000000040110e <+8>:     mov    DWORD PTR [rbp-0x14],edi
   0x0000000000401111 <+11>:    mov    QWORD PTR [rbp-0x20],rsi
   0x0000000000401115 <+15>:    mov    DWORD PTR [rbp-0x4],0x2262c96b
   0x000000000040111c <+22>:    mov    eax,DWORD PTR [rbp-0x4]
   0x000000000040111f <+25>:    pop    rbp
   0x0000000000401120 <+26>:    ret
End of assembler dump.
```
- Creamos otro `breakpoint` en la línea 25 para que se detenga la ejecución del programa.
```bash
(gdb) break *(main+25)
Breakpoint 2 at 0x40111f
(gdb) continue 
Continuing.

Breakpoint 2, 0x000000000040111f in main ()
(gdb) disassemble main 
Dump of assembler code for function main:
   0x0000000000401106 <+0>:     endbr64
   0x000000000040110a <+4>:     push   rbp
   0x000000000040110b <+5>:     mov    rbp,rsp
   0x000000000040110e <+8>:     mov    DWORD PTR [rbp-0x14],edi
   0x0000000000401111 <+11>:    mov    QWORD PTR [rbp-0x20],rsi
   0x0000000000401115 <+15>:    mov    DWORD PTR [rbp-0x4],0x2262c96b
   0x000000000040111c <+22>:    mov    eax,DWORD PTR [rbp-0x4]
=> 0x000000000040111f <+25>:    pop    rbp
   0x0000000000401120 <+26>:    ret
End of assembler dump.
```
- Inspeccionamos el contenido del registro EAX en este punto ejecutando.
```bash
(gdb) info registers eax
eax            0x2262c96b          576899435
```
- Sin embargo, esta no es nuestra bandera. El comando `file` indica el uso de una representación `little-endian`, lo que implica el almacenamiento de los bytes en orden inverso. Siguiendo la sugerencia del reto, inspeccionamos el contenido real de la memoria.
```bash
(gdb) x/4xb $rbp-4
0x7fffffffdcfc: 0x6b    0xc9    0x62    0x22
(gdb) c
Continuing.
[Inferior 1 (process 23410) exited with code 0153]
(gdb) quit

┌──(armando㉿kali)-[~/picoCTF/reversing/GDBbabystep3]
└─$ 
```
- Y ya obtenemos la bandera en el formato requerido por el reto.
```bash
picoCTF{0x6bc96222}
```

## Notas Adicionales
## Referencias