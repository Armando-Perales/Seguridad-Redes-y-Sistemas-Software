## Objetivo
Can you figure out what is in the `eax` register? Put your answer in the picoCTF flag format: `picoCTF{n}` where `n` is the contents of the `eax` register in the decimal number base. If the answer was `0x11` your flag would be `picoCTF{17}`. Download the assembly dump [here](https://artifacts.picoctf.net/c/510/disassembler-dump0_b.txt).
## Solución

```bash
┌──(armando㉿kali)-[~/picoCTF/reversing/Bit-O-Asm-2]
└─$ ls
disassembler-dump0_b.txt

┌──(armando㉿kali)-[~/picoCTF/reversing/Bit-O-Asm-2]
└─$ file disassembler-dump0_b.txt 
disassembler-dump0_b.txt: ASCII text

┌──(armando㉿kali)-[~/picoCTF/reversing/Bit-O-Asm-2]
└─$ cat disassembler-dump0_b.txt 
<+0>:     endbr64 
<+4>:     push   rbp
<+5>:     mov    rbp,rsp
<+8>:     mov    DWORD PTR [rbp-0x14],edi
<+11>:    mov    QWORD PTR [rbp-0x20],rsi
<+15>:    mov    DWORD PTR [rbp-0x4],0x9fe1a
<+22>:    mov    eax,DWORD PTR [rbp-0x4]
<+25>:    pop    rbp
<+26>:    ret
```
- Ignoramos la mayoría de las líneas iniciales hasta llegar a la línea <+15>, cuando 0x9fe1a se pasa al registro de puntero base. En la línea <+22>, movemos este valor desde el puntero base en esta dirección a `eax` y encontramos nuestro valor almacenado en `eax`. En este punto, convertimos 0x9fe1a en decimal y descubrimos que representa el número 654874 y esto seria la bandera.
```bash
┌──(armando㉿kali)-[~/picoCTF/reversing/Bit-O-Asm-2]
└─$ python3
Python 3.12.6 (main, Sep  7 2024, 14:20:15) [GCC 14.2.0] on linux
Type "help", "copyright", "credits" or "license" for more information.
>>> 0x9fe1a
654874
>>> 

┌──(armando㉿kali)-[~/picoCTF/reversing/Bit-O-Asm-2]
└─$                     
```
- Por lo tanto la bandera quedaría de la siguiente forma.
```bash
picoCTF{654874}
```

## Notas Adicionales
## Referencias