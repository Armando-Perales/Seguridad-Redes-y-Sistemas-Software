## Objetivo
Can you figure out how this program works to get the flag? Connect to the program with netcat: `$ nc saturn.picoctf.net 62981` The program's source code can be downloaded [here](https://artifacts.picoctf.net/c/528/picker-IV.c). The binary can be downloaded [here](https://artifacts.picoctf.net/c/528/picker-IV).
## Solución

```bash
┌──(armando㉿kali)-[~/picoCTF/reversing/picker4]
└─$ ls
picker-IV  picker-IV.c

┌──(armando㉿kali)-[~/picoCTF/reversing/picker4]
└─$ nano picker-IV.c  
```

```C
#include <stdio.h>
#include <stdlib.h>
#include <signal.h>
#include <unistd.h>


void print_segf_message(){
  printf("Segfault triggered! Exiting.\n");
  sleep(15);
  exit(SIGSEGV);
}

int win() {
  FILE *fptr;
  char c;

  printf("You won!\n");
  // Open file
  fptr = fopen("flag.txt", "r");
  if (fptr == NULL)
  {
      printf("Cannot open file.\n");
      exit(0);
  }

  // Read contents from file
  c = fgetc(fptr);
  while (c != EOF)
  {
      printf ("%c", c);
      c = fgetc(fptr);
  }

  printf("\n");
  fclose(fptr);
}

int main() {
  signal(SIGSEGV, print_segf_message);
  setvbuf(stdout, NULL, _IONBF, 0); // _IONBF = Unbuffered

  unsigned int val;
  printf("Enter the address in hex to jump to, excluding '0x': ");
  scanf("%x", &val);
  printf("You input 0x%x\n", val);

  void (*foo)(void) = (void (*)())val;
  foo();
}

```
- Vemos que es un archivo ejecutable por lo que le añadimos los permisos de ejecución.
```bash
┌──(armando㉿kali)-[~/picoCTF/reversing/picker4]
└─$ file picker-IV           
picker-IV: ELF 64-bit LSB executable, x86-64, version 1 (SYSV), dynamically linked, interpreter /lib64/ld-linux-x86-64.so.2, BuildID[sha1]=12b33c5ff389187551aae5774324da558cee006c, for GNU/Linux 3.2.0, not stripped

┌──(armando㉿kali)-[~/picoCTF/reversing/picker4]
└─$ chmod +x picker-IV

┌──(armando㉿kali)-[~/picoCTF/reversing/picker4]
└─$ ./picker-IV 
Enter the address in hex to jump to, excluding '0x': ^C

```
- Entramos al servidor que nos dan y aquí le enviamos la dirección donde se encuentra la función `win`.
```bash
┌──(armando㉿kali)-[~/picoCTF/reversing/picker4]
└─$ nc saturn.picoctf.net 62981
Enter the address in hex to jump to, excluding '0x': 40129e
You input 0x40129e
You won!
picoCTF{n3v3r_jump_t0_u53r_5uppl13d_4ddr35535_14bc5444}

┌──(armando㉿kali)-[~/picoCTF/reversing/picker4]
└─$ 
```
- Para encontrar la dirección donde se encuentra la función `win` hay 2 formas:
### Opción 1
- Utilizando el comando `readelf` junto con el comando `grep`.
```bash
┌──(armando㉿kali)-[~/picoCTF/reversing/picker4]
└─$ readelf -a picker-IV | grep win
No processor specific unwind information to decode
    63: 000000000040129e   150 FUNC    GLOBAL DEFAULT   15 win
```

### Opción 2
- Utilizando la herramienta `gdb` y enviándole que nos de la `info functions`.
```

```bash
┌──(armando㉿kali)-[~/picoCTF/reversing/picker4]
└─$ gdb picker-IV 
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
Reading symbols from picker-IV...
(No debugging symbols found in picker-IV)
(gdb) info functions
All defined functions:

Non-debugging symbols:
0x0000000000401000  _init
0x00000000004010e0  putchar@plt
0x00000000004010f0  puts@plt
0x0000000000401100  fclose@plt
0x0000000000401110  printf@plt
0x0000000000401120  fgetc@plt
0x0000000000401130  signal@plt
0x0000000000401140  setvbuf@plt
0x0000000000401150  fopen@plt
0x0000000000401160  __isoc99_scanf@plt
0x0000000000401170  exit@plt
0x0000000000401180  sleep@plt
0x0000000000401190  _start
0x00000000004011c0  _dl_relocate_static_pie
0x00000000004011d0  deregister_tm_clones
0x0000000000401200  register_tm_clones
0x0000000000401240  __do_global_dtors_aux
0x0000000000401270  frame_dummy
0x0000000000401276  print_segf_message
0x000000000040129e  win
0x0000000000401334  main
0x00000000004013d0  __libc_csu_init
0x0000000000401440  __libc_csu_fini
0x0000000000401448  _fini
(gdb) 
```

## Notas Adicionales
readelf -a picker-IV | grep win
	readelf - Muestra información acerca de archivos ELF
## Referencias