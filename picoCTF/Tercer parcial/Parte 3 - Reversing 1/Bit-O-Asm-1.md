## Objetivo
Can you figure out what is in the `eax` register? Put your answer in the picoCTF flag format: `picoCTF{n}` where `n` is the contents of the `eax` register in the decimal number base. If the answer was `0x11` your flag would be `picoCTF{17}`. Download the assembly dump [here](https://artifacts.picoctf.net/c/509/disassembler-dump0_a.txt).
## Solución

```bash
┌──(armando㉿kali)-[~/picoCTF/reversing/Bit-O-Asm-1]
└─$ ls
disassembler-dump0_a.txt

┌──(armando㉿kali)-[~/picoCTF/reversing/Bit-O-Asm-1]
└─$ file disassembler-dump0_a.txt 
disassembler-dump0_a.txt: ASCII text

┌──(armando㉿kali)-[~/picoCTF/reversing/Bit-O-Asm-1]
└─$ cat disassembler-dump0_a.txt 
<+0>:     endbr64 
<+4>:     push   rbp
<+5>:     mov    rbp,rsp
<+8>:     mov    DWORD PTR [rbp-0x4],edi
<+11>:    mov    QWORD PTR [rbp-0x10],rsi
<+15>:    mov    eax,0x30
<+20>:    pop    rbp
<+21>:    ret
```
- Convertimos el valor hexadecimal de `eax`.
```bash
┌──(armando㉿kali)-[~/picoCTF/reversing/Bit-O-Asm-1]
└─$ python3         
Python 3.12.6 (main, Sep  7 2024, 14:20:15) [GCC 14.2.0] on linux
Type "help", "copyright", "credits" or "license" for more information.
>>> int(0x30)
48
>>> 

┌──(armando㉿kali)-[~/picoCTF/reversing/Bit-O-Asm-1]
└─$ 
```
- Por lo tanto la bandera quedaría de la siguiente forma.
```bash
picoCTF{48}
```

## Notas Adicionales
## Referencias