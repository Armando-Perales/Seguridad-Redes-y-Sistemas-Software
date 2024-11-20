## Objetivo
Can you get the flag? Reverse engineer this [binary](https://artifacts.picoctf.net/c/205/unpackme-upx).
## Solución

```bash
┌──(armando㉿kali)-[~/picoCTF/reversing/unpackme]
└─$ ls -la
total 988
drwxrwxr-x  2 armando armando    4096 Nov 16 20:20 .
drwxrwxr-x 25 armando armando    4096 Nov 16 20:16 ..
-rw-rw-r--  1 armando armando 1002528 Aug  4  2023 unpackme-upx

┌──(armando㉿kali)-[~/picoCTF/reversing/unpackme]
└─$ file unpackme-upx 
unpackme-upx: ELF 64-bit LSB executable, x86-64, version 1 (GNU/Linux), statically linked, no section header
```
- Descomprimimos el archivo que nos dieron, despues abrimos el binario con la herramienta de `ghidra`.
```bash
┌──(armando㉿kali)-[~/picoCTF/reversing/unpackme]
└─$ upx -d unpackme-upx 
                       Ultimate Packer for eXecutables
                          Copyright (C) 1996 - 2024
UPX 4.2.4       Markus Oberhumer, Laszlo Molnar & John Reiser    May 9th 2024

        File size         Ratio      Format      Name
   --------------------   ------   -----------   -----------
   1006445 <-    379188   37.68%   linux/amd64   unpackme-upx

Unpacked 1 file.

┌──(armando㉿kali)-[~/picoCTF/reversing/unpackme]
└─$ ghidra         
Picked up _JAVA_OPTIONS: -Dawt.useSystemAAFontSettings=on -Dswing.aatext=true
Picked up _JAVA_OPTIONS: -Dawt.useSystemAAFontSettings=on -Dswing.aatext=true
```
- Una vez abierto el programa buscamos la función del `main`.
```c
undefined8 main(void)

{
  long in_FS_OFFSET;
  int iStack_44;
  undefined8 uStack_40;
  undefined8 uStack_38;
  undefined8 uStack_30;
  undefined8 uStack_28;
  undefined4 uStack_20;
  undefined2 uStack_1c;
  long lStack_10;
  
  lStack_10 = *(long *)(in_FS_OFFSET + 0x28);
  uStack_38 = 0x4c75257240343a41;
  uStack_30 = 0x30623e306b6d4146;
  uStack_28 = 0x6865666430486637;
  uStack_20 = 0x36636433;
  uStack_1c = 0x4e;
  printf(&UNK_004b3004);
  __isoc99_scanf(&UNK_004b3020,&iStack_44);
  if (iStack_44 == 0xb83cb) {
    uStack_40 = rotate_encrypt(0,&uStack_38);
    fputs(uStack_40,stdout);
    putchar(10);
    free(uStack_40);
  }
  else {
    puts(&UNK_004b3023);
  }
  if (lStack_10 != *(long *)(in_FS_OFFSET + 0x28)) {
                    /* WARNING: Subroutine does not return */
    __stack_chk_fail();
  }
  return 0;
}
```
- Notamos que si el `local_44` es igual al valor `0xb83cb` (`754635`)nos dará  la bandera, por lo que ejecutamos el programa y le enviamos el valor solicitado.
```bash
┌──(armando㉿kali)-[~/picoCTF/reversing/unpackme]
└─$ chmod +x unpackme-upx 

┌──(armando㉿kali)-[~/picoCTF/reversing/unpackme]
└─$ ls -la               
total 988
drwxrwxr-x  2 armando armando    4096 Nov 16 20:20 .
drwxrwxr-x 25 armando armando    4096 Nov 16 20:16 ..
-rwxrwxr-x  1 armando armando 1002528 Aug  4  2023 unpackme-upx

┌──(armando㉿kali)-[~/picoCTF/reversing/unpackme]
└─$ ./unpackme-upx       
What's my favorite number? 754635
picoCTF{up><_m3_f7w_5769b54e}

┌──(armando㉿kali)-[~/picoCTF/reversing/unpackme]
└─$ 

```

## Notas Adicionales
## Referencias
- [UPX](https://en.wikipedia.org/wiki/UPX)