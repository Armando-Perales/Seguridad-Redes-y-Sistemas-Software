## Objetivo
We have recovered a [binary](https://jupiter.challenges.picoctf.org/static/7aa5f383ec616fe9d72c2ffe1fabd0d9/rev) and a [text file](https://jupiter.challenges.picoctf.org/static/7aa5f383ec616fe9d72c2ffe1fabd0d9/rev_this). Can you reverse the flag.
## Solución

```bash
┌──(armando㉿kali)-[~/picoCTF/reversing/reversecipher]
└─$ ls -la
total 32
drwxrwxr-x  2 armando armando  4096 Nov  6 11:18 .
drwxrwxr-x 19 armando armando  4096 Nov  6 11:18 ..
-rw-rw-r--  1 armando armando 16856 Oct 26  2020 rev
-rw-rw-r--  1 armando armando    24 Oct 26  2020 rev_this

┌──(armando㉿kali)-[~/picoCTF/reversing/reversecipher]
└─$ file rev           
rev: ELF 64-bit LSB pie executable, x86-64, version 1 (SYSV), dynamically linked, interpreter /lib64/ld-linux-x86-64.so.2, for GNU/Linux 3.2.0, BuildID[sha1]=523d51973c11197605c76f84d4afb0fe9e59338c, not stripped

┌──(armando㉿kali)-[~/picoCTF/reversing/reversecipher]
└─$ file rev_this 
rev_this: ASCII text, with no line terminators

┌──(armando㉿kali)-[~/picoCTF/reversing/reversecipher]
└─$ chmod +x rev    

┌──(armando㉿kali)-[~/picoCTF/reversing/reversecipher]
└─$ ./rev    
No flag found, please make sure this is run on the server
zsh: segmentation fault  ./rev

┌──(armando㉿kali)-[~/picoCTF/reversing/reversecipher]
└─$ cat rev_this      
picoCTF{w1{1wq84fb<1>49}                                                                                                                    
┌──(armando㉿kali)-[~/picoCTF/reversing/reversecipher]
└─$ gdb -q rev    
Reading symbols from rev...
(No debugging symbols found in rev)
(gdb) info functions
All defined functions:

Non-debugging symbols:
0x0000000000001000  _init
0x0000000000001030  puts@plt
0x0000000000001040  fread@plt
0x0000000000001050  fclose@plt
0x0000000000001060  fputc@plt
0x0000000000001070  fopen@plt
0x0000000000001080  exit@plt
0x0000000000001090  __cxa_finalize@plt
0x00000000000010a0  _start
0x00000000000010d0  deregister_tm_clones
0x0000000000001100  register_tm_clones
0x0000000000001140  __do_global_dtors_aux
0x0000000000001180  frame_dummy
0x0000000000001185  main
0x00000000000012d0  __libc_csu_init
0x0000000000001330  __libc_csu_fini
0x0000000000001334  _fini
(gdb) disassemble main
Dump of assembler code for function main:
   0x0000000000001185 <+0>:     push   %rbp
   0x0000000000001186 <+1>:     mov    %rsp,%rbp
   0x0000000000001189 <+4>:     sub    $0x50,%rsp
   0x000000000000118d <+8>:     lea    0xe74(%rip),%rsi        # 0x2008
   0x0000000000001194 <+15>:    lea    0xe6f(%rip),%rdi        # 0x200a
   0x000000000000119b <+22>:    call   0x1070 <fopen@plt>
   0x00000000000011a0 <+27>:    mov    %rax,-0x18(%rbp)
   0x00000000000011a4 <+31>:    lea    0xe68(%rip),%rsi        # 0x2013
   0x00000000000011ab <+38>:    lea    0xe63(%rip),%rdi        # 0x2015
   0x00000000000011b2 <+45>:    call   0x1070 <fopen@plt>
   0x00000000000011b7 <+50>:    mov    %rax,-0x20(%rbp)
   0x00000000000011bb <+54>:    cmpq   $0x0,-0x18(%rbp)
   0x00000000000011c0 <+59>:    jne    0x11ce <main+73>
   0x00000000000011c2 <+61>:    lea    0xe57(%rip),%rdi        # 0x2020
   0x00000000000011c9 <+68>:    call   0x1030 <puts@plt>
   0x00000000000011ce <+73>:    cmpq   $0x0,-0x20(%rbp)
   0x00000000000011d3 <+78>:    jne    0x11e1 <main+92>
   0x00000000000011d5 <+80>:    lea    0xe7e(%rip),%rdi        # 0x205a
   0x00000000000011dc <+87>:    call   0x1030 <puts@plt>
   0x00000000000011e1 <+92>:    mov    -0x18(%rbp),%rdx
   0x00000000000011e5 <+96>:    lea    -0x50(%rbp),%rax
   0x00000000000011e9 <+100>:   mov    %rdx,%rcx
   0x00000000000011ec <+103>:   mov    $0x1,%edx
   0x00000000000011f1 <+108>:   mov    $0x18,%esi
   0x00000000000011f6 <+113>:   mov    %rax,%rdi
   0x00000000000011f9 <+116>:   call   0x1040 <fread@plt>
   0x00000000000011fe <+121>:   mov    %eax,-0x24(%rbp)
   0x0000000000001201 <+124>:   cmpl   $0x0,-0x24(%rbp)
   0x0000000000001205 <+128>:   jg     0x1211 <main+140>
   0x0000000000001207 <+130>:   mov    $0x0,%edi
   0x000000000000120c <+135>:   call   0x1080 <exit@plt>
   0x0000000000001211 <+140>:   movl   $0x0,-0x8(%rbp)
   0x0000000000001218 <+147>:   jmp    0x123d <main+184>
   0x000000000000121a <+149>:   mov    -0x8(%rbp),%eax
   0x000000000000121d <+152>:   cltq
   0x000000000000121f <+154>:   movzbl -0x50(%rbp,%rax,1),%eax
   0x0000000000001224 <+159>:   mov    %al,-0x1(%rbp)
   0x0000000000001227 <+162>:   movsbl -0x1(%rbp),%eax
   0x000000000000122b <+166>:   mov    -0x20(%rbp),%rdx
   0x000000000000122f <+170>:   mov    %rdx,%rsi
   0x0000000000001232 <+173>:   mov    %eax,%edi
   0x0000000000001234 <+175>:   call   0x1060 <fputc@plt>
   0x0000000000001239 <+180>:   addl   $0x1,-0x8(%rbp)
   0x000000000000123d <+184>:   cmpl   $0x7,-0x8(%rbp)
   0x0000000000001241 <+188>:   jle    0x121a <main+149>
   0x0000000000001243 <+190>:   movl   $0x8,-0xc(%rbp)
   0x000000000000124a <+197>:   jmp    0x128f <main+266>
   0x000000000000124c <+199>:   mov    -0xc(%rbp),%eax
   0x000000000000124f <+202>:   cltq
   0x0000000000001251 <+204>:   movzbl -0x50(%rbp,%rax,1),%eax
--Type <RET> for more, q to quit, c to continue without paging--
```
- Descargamos la herramienta `ghidra` y la abrimos con el archivo `rev`.
```bash
┌──(armando㉿kali)-[~/picoCTF/reversing/reversecipher]
└─$ sudo apt install ghidra
...
┌──(armando㉿kali)-[~/picoCTF/reversing/reversecipher]
└─$ ghidra    
Picked up _JAVA_OPTIONS: -Dawt.useSystemAAFontSettings=on -Dswing.aatext=true
Picked up _JAVA_OPTIONS: -Dawt.useSystemAAFontSettings=on -Dswing.aatext=true
```
- Buscamos el código `main` para ver cuales fueron las acciones que realizo para codificar la bandera. 
```c
void main(void)

{
  size_t sVar1;
  char local_58 [23];
  char local_41;
  int local_2c;
  FILE *local_28;
  FILE *local_20;
  uint local_14;
  int local_10;
  char local_9;
  
  local_20 = fopen("flag.txt","r");
  local_28 = fopen("rev_this","a");
  if (local_20 == (FILE *)0x0) {
    puts("No flag found, please make sure this is run on the server");
  }
  if (local_28 == (FILE *)0x0) {
    puts("please run this on the server");
  }
  sVar1 = fread(local_58,0x18,1,local_20);
  local_2c = (int)sVar1;
  if ((int)sVar1 < 1) {
                    /* WARNING: Subroutine does not return */
    exit(0);
  }
  for (local_10 = 0; local_10 < 8; local_10 = local_10 + 1) {
    local_9 = local_58[local_10];
    fputc((int)local_9,local_28);
  }
  for (local_14 = 8; (int)local_14 < 0x17; local_14 = local_14 + 1) {
    if ((local_14 & 1) == 0) {
      local_9 = local_58[(int)local_14] + '\x05';
    }
    else {
      local_9 = local_58[(int)local_14] + -2;
    }
    fputc((int)local_9,local_28);
  }
  local_9 = local_41;
  fputc((int)local_41,local_28);
  fclose(local_28);
  fclose(local_20);
  return;

```
- Creamos un código en Python que hace lo contrario a la función del `main` para decodificar la bandera.
```bash
┌──(armando㉿kali)-[~/picoCTF/reversing/reversecipher]
└─$ nano solve.py
```
```python       
rev = open('rev_this').read()
flag = ''
for i in range(8):
        flag += rev[i]
for j in range(8,24):
        if j&1 ==0:
                flag += chr(ord(rev[j]) - 5)
        else:
                flag += chr(ord(rev[j]) + 2)
flag += rev[23]

print(flag)
```
- Ejecutamos el programa y ya nos muestra la bandera ya decodificada.
```bash
┌──(armando㉿kali)-[~/picoCTF/reversing/reversecipher]
└─$ python3 solve.py
picoCTF{r3v3rs36ad73964}

┌──(armando㉿kali)-[~/picoCTF/reversing/reversecipher]
└─$ 
```

## Notas Adicionales
## Referencias