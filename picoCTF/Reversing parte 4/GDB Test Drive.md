## Objetivo
Can you get the flag? Download this [binary](https://artifacts.picoctf.net/c/85/gdbme). Here's the test drive instructions:

- `$ chmod +x gdbme`
- `$ gdb gdbme`
- `(gdb) layout asm`
- `(gdb) break *(main+99)`
- `(gdb) run`
- `(gdb) jump *(main+104)`
## Solución

```bash
┌──(armando㉿kali)-[~/picoCTF/reversing/GDBTestDrive]
└─$ ls -la 
total 28
drwxrwxr-x  2 armando armando  4096 Nov  6 10:43 .
drwxrwxr-x 17 armando armando  4096 Nov  6 10:42 ..
-rw-rw-r--  1 armando armando 17048 Aug  4  2023 gdbme

┌──(armando㉿kali)-[~/picoCTF/reversing/GDBTestDrive]
└─$ chmod +x gdbme  

┌──(armando㉿kali)-[~/picoCTF/reversing/GDBTestDrive]
└─$ ls -la        
total 28
drwxrwxr-x  2 armando armando  4096 Nov  6 10:43 .
drwxrwxr-x 17 armando armando  4096 Nov  6 10:42 ..
-rwxrwxr-x  1 armando armando 17048 Aug  4  2023 gdbme

┌──(armando㉿kali)-[~/picoCTF/reversing/GDBTestDrive]
└─$ ./gdbme 
^C
```
- Abrimos el archivo con la herramienta `gdb` para revisar el código. 
```bash
┌──(armando㉿kali)-[~/picoCTF/reversing/GDBTestDrive]
└─$ gdb -q gdbme                    
Reading symbols from gdbme...
(No debugging symbols found in gdbme)
(gdb) info functions
All defined functions:

Non-debugging symbols:
0x0000000000001000  _init
0x00000000000010a0  __cxa_finalize@plt
0x00000000000010b0  free@plt
0x00000000000010c0  putchar@plt
0x00000000000010d0  strlen@plt
0x00000000000010e0  __stack_chk_fail@plt
0x00000000000010f0  fputs@plt
0x0000000000001100  strdup@plt
0x0000000000001110  sleep@plt
0x0000000000001120  _start
0x0000000000001150  deregister_tm_clones
0x0000000000001180  register_tm_clones
0x00000000000011c0  __do_global_dtors_aux
0x0000000000001200  frame_dummy
0x0000000000001209  rotate_encrypt
0x00000000000012c7  main
0x0000000000001390  __libc_csu_init
0x0000000000001400  __libc_csu_fini
0x0000000000001408  _fini
(gdb) disassemble main
Dump of assembler code for function main:
   0x00000000000012c7 <+0>:     endbr64
   0x00000000000012cb <+4>:     push   %rbp
   0x00000000000012cc <+5>:     mov    %rsp,%rbp
   0x00000000000012cf <+8>:     sub    $0x50,%rsp
   0x00000000000012d3 <+12>:    mov    %edi,-0x44(%rbp)
   0x00000000000012d6 <+15>:    mov    %rsi,-0x50(%rbp)
   0x00000000000012da <+19>:    mov    %fs:0x28,%rax
   0x00000000000012e3 <+28>:    mov    %rax,-0x8(%rbp)
   0x00000000000012e7 <+32>:    xor    %eax,%eax
   0x00000000000012e9 <+34>:    movabs $0x4c75257240343a41,%rax
   0x00000000000012f3 <+44>:    movabs $0x4362383846336235,%rdx
   0x00000000000012fd <+54>:    mov    %rax,-0x30(%rbp)
   0x0000000000001301 <+58>:    mov    %rdx,-0x28(%rbp)
   0x0000000000001305 <+62>:    movabs $0x6030624760433530,%rax
   0x000000000000130f <+72>:    movabs $0x4e32676662346668,%rdx
   0x0000000000001319 <+82>:    mov    %rax,-0x20(%rbp)
   0x000000000000131d <+86>:    mov    %rdx,-0x18(%rbp)
   0x0000000000001321 <+90>:    movb   $0x0,-0x10(%rbp)
   0x0000000000001325 <+94>:    mov    $0x186a0,%edi
   0x000000000000132a <+99>:    call   0x1110 <sleep@plt>
   0x000000000000132f <+104>:   lea    -0x30(%rbp),%rax
   0x0000000000001333 <+108>:   mov    %rax,%rsi
   0x0000000000001336 <+111>:   mov    $0x0,%edi
   0x000000000000133b <+116>:   call   0x1209 <rotate_encrypt>
   0x0000000000001340 <+121>:   mov    %rax,-0x38(%rbp)
   0x0000000000001344 <+125>:   mov    0x2cc5(%rip),%rdx        # 0x4010 <stdout@@GLIBC_2.2.5>
   0x000000000000134b <+132>:   mov    -0x38(%rbp),%rax
   0x000000000000134f <+136>:   mov    %rdx,%rsi
   0x0000000000001352 <+139>:   mov    %rax,%rdi
   0x0000000000001355 <+142>:   call   0x10f0 <fputs@plt>
   0x000000000000135a <+147>:   mov    $0xa,%edi
   0x000000000000135f <+152>:   call   0x10c0 <putchar@plt>
   0x0000000000001364 <+157>:   mov    -0x38(%rbp),%rax
   0x0000000000001368 <+161>:   mov    %rax,%rdi
   0x000000000000136b <+164>:   call   0x10b0 <free@plt>
   0x0000000000001370 <+169>:   mov    $0x0,%eax
   0x0000000000001375 <+174>:   mov    -0x8(%rbp),%rcx
   0x0000000000001379 <+178>:   xor    %fs:0x28,%rcx
   0x0000000000001382 <+187>:   je     0x1389 <main+194>
   0x0000000000001384 <+189>:   call   0x10e0 <__stack_chk_fail@plt>
   0x0000000000001389 <+194>:   leave
   0x000000000000138a <+195>:   ret
End of assembler dump.
```
- Le modificamos la forma en que presenta el código para un mejor entendimiento del lenguaje.
```bash
(gdb) set disassembly-flavor intel
(gdb) disassemble main
Dump of assembler code for function main:
   0x00000000000012c7 <+0>:     endbr64
   0x00000000000012cb <+4>:     push   rbp
   0x00000000000012cc <+5>:     mov    rbp,rsp
   0x00000000000012cf <+8>:     sub    rsp,0x50
   0x00000000000012d3 <+12>:    mov    DWORD PTR [rbp-0x44],edi
   0x00000000000012d6 <+15>:    mov    QWORD PTR [rbp-0x50],rsi
   0x00000000000012da <+19>:    mov    rax,QWORD PTR fs:0x28
   0x00000000000012e3 <+28>:    mov    QWORD PTR [rbp-0x8],rax
   0x00000000000012e7 <+32>:    xor    eax,eax
   0x00000000000012e9 <+34>:    movabs rax,0x4c75257240343a41
   0x00000000000012f3 <+44>:    movabs rdx,0x4362383846336235
   0x00000000000012fd <+54>:    mov    QWORD PTR [rbp-0x30],rax
   0x0000000000001301 <+58>:    mov    QWORD PTR [rbp-0x28],rdx
   0x0000000000001305 <+62>:    movabs rax,0x6030624760433530
   0x000000000000130f <+72>:    movabs rdx,0x4e32676662346668
   0x0000000000001319 <+82>:    mov    QWORD PTR [rbp-0x20],rax
   0x000000000000131d <+86>:    mov    QWORD PTR [rbp-0x18],rdx
   0x0000000000001321 <+90>:    mov    BYTE PTR [rbp-0x10],0x0
   0x0000000000001325 <+94>:    mov    edi,0x186a0
   0x000000000000132a <+99>:    call   0x1110 <sleep@plt>
   0x000000000000132f <+104>:   lea    rax,[rbp-0x30]
   0x0000000000001333 <+108>:   mov    rsi,rax
   0x0000000000001336 <+111>:   mov    edi,0x0
   0x000000000000133b <+116>:   call   0x1209 <rotate_encrypt>
   0x0000000000001340 <+121>:   mov    QWORD PTR [rbp-0x38],rax
   0x0000000000001344 <+125>:   mov    rdx,QWORD PTR [rip+0x2cc5]        # 0x4010 <stdout@@GLIBC_2.2.5>
   0x000000000000134b <+132>:   mov    rax,QWORD PTR [rbp-0x38]
   0x000000000000134f <+136>:   mov    rsi,rdx
   0x0000000000001352 <+139>:   mov    rdi,rax
   0x0000000000001355 <+142>:   call   0x10f0 <fputs@plt>
   0x000000000000135a <+147>:   mov    edi,0xa
   0x000000000000135f <+152>:   call   0x10c0 <putchar@plt>
   0x0000000000001364 <+157>:   mov    rax,QWORD PTR [rbp-0x38]
   0x0000000000001368 <+161>:   mov    rdi,rax
   0x000000000000136b <+164>:   call   0x10b0 <free@plt>
   0x0000000000001370 <+169>:   mov    eax,0x0
   0x0000000000001375 <+174>:   mov    rcx,QWORD PTR [rbp-0x8]
   0x0000000000001379 <+178>:   xor    rcx,QWORD PTR fs:0x28
   0x0000000000001382 <+187>:   je     0x1389 <main+194>
   0x0000000000001384 <+189>:   call   0x10e0 <__stack_chk_fail@plt>
   0x0000000000001389 <+194>:   leave
   0x000000000000138a <+195>:   ret
End of assembler dump.
```
- Creamos un `breakpoint` en la línea 99 para que se detenga la ejecución del programa.
```bash
(gdb) break *(main+99)
Breakpoint 1 at 0x132a
(gdb) info breakpoints 
Num     Type           Disp Enb Address            What
1       breakpoint     keep y   0x000000000000132a <main+99>
(gdb) run
Starting program: /home/armando/picoCTF/reversing/GDBTestDrive/gdbme 
[Thread debugging using libthread_db enabled]
Using host libthread_db library "/lib/x86_64-linux-gnu/libthread_db.so.1".

Breakpoint 1, 0x000055555555532a in main ()
(gdb) disassemble main
Dump of assembler code for function main:
   0x00005555555552c7 <+0>:     endbr64
   0x00005555555552cb <+4>:     push   rbp
   0x00005555555552cc <+5>:     mov    rbp,rsp
   0x00005555555552cf <+8>:     sub    rsp,0x50
   0x00005555555552d3 <+12>:    mov    DWORD PTR [rbp-0x44],edi
   0x00005555555552d6 <+15>:    mov    QWORD PTR [rbp-0x50],rsi
   0x00005555555552da <+19>:    mov    rax,QWORD PTR fs:0x28
   0x00005555555552e3 <+28>:    mov    QWORD PTR [rbp-0x8],rax
   0x00005555555552e7 <+32>:    xor    eax,eax
   0x00005555555552e9 <+34>:    movabs rax,0x4c75257240343a41
   0x00005555555552f3 <+44>:    movabs rdx,0x4362383846336235
   0x00005555555552fd <+54>:    mov    QWORD PTR [rbp-0x30],rax
   0x0000555555555301 <+58>:    mov    QWORD PTR [rbp-0x28],rdx
   0x0000555555555305 <+62>:    movabs rax,0x6030624760433530
   0x000055555555530f <+72>:    movabs rdx,0x4e32676662346668
   0x0000555555555319 <+82>:    mov    QWORD PTR [rbp-0x20],rax
   0x000055555555531d <+86>:    mov    QWORD PTR [rbp-0x18],rdx
   0x0000555555555321 <+90>:    mov    BYTE PTR [rbp-0x10],0x0
   0x0000555555555325 <+94>:    mov    edi,0x186a0
=> 0x000055555555532a <+99>:    call   0x555555555110 <sleep@plt>
   0x000055555555532f <+104>:   lea    rax,[rbp-0x30]
   0x0000555555555333 <+108>:   mov    rsi,rax
   0x0000555555555336 <+111>:   mov    edi,0x0
   0x000055555555533b <+116>:   call   0x555555555209 <rotate_encrypt>
   0x0000555555555340 <+121>:   mov    QWORD PTR [rbp-0x38],rax
   0x0000555555555344 <+125>:   mov    rdx,QWORD PTR [rip+0x2cc5]        # 0x555555558010 <stdout@@GLIBC_2.2.5>
   0x000055555555534b <+132>:   mov    rax,QWORD PTR [rbp-0x38]
   0x000055555555534f <+136>:   mov    rsi,rdx
   0x0000555555555352 <+139>:   mov    rdi,rax
   0x0000555555555355 <+142>:   call   0x5555555550f0 <fputs@plt>
   0x000055555555535a <+147>:   mov    edi,0xa
   0x000055555555535f <+152>:   call   0x5555555550c0 <putchar@plt>
   0x0000555555555364 <+157>:   mov    rax,QWORD PTR [rbp-0x38]
   0x0000555555555368 <+161>:   mov    rdi,rax
   0x000055555555536b <+164>:   call   0x5555555550b0 <free@plt>
   0x0000555555555370 <+169>:   mov    eax,0x0
   0x0000555555555375 <+174>:   mov    rcx,QWORD PTR [rbp-0x8]
   0x0000555555555379 <+178>:   xor    rcx,QWORD PTR fs:0x28
   0x0000555555555382 <+187>:   je     0x555555555389 <main+194>
   0x0000555555555384 <+189>:   call   0x5555555550e0 <__stack_chk_fail@plt>
   0x0000555555555389 <+194>:   leave
   0x000055555555538a <+195>:   ret
End of assembler dump.
```
- Hacemos que salte hasta la línea 104 para evitar el `sleep` y de esta manera muestre la bandera.
```
(gdb) jump *(main+104)
Continuing at 0x55555555532f.
picoCTF{d3bugg3r_dr1v3_197c378a}
[Inferior 1 (process 25413) exited normally]
(gdb) 

```

## Notas Adicionales
## Referencias