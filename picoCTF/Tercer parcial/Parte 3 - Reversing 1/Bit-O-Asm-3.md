## Objetivo
Can you figure out what is in the `eax` register? Put your answer in the picoCTF flag format: `picoCTF{n}` where `n` is the contents of the `eax` register in the decimal number base. If the answer was `0x11` your flag would be `picoCTF{17}`. Download the assembly dump [here](https://artifacts.picoctf.net/c/530/disassembler-dump0_c.txt).
## Solución

```bash
┌──(armando㉿kali)-[~/picoCTF/reversing/Bit-O-Asm-3]
└─$ ls
disassembler-dump0_c.txt

┌──(armando㉿kali)-[~/picoCTF/reversing/Bit-O-Asm-3]
└─$ file disassembler-dump0_c.txt 
disassembler-dump0_c.txt: ASCII text

┌──(armando㉿kali)-[~/picoCTF/reversing/Bit-O-Asm-3]
└─$ cat disassembler-dump0_c.txt 
<+0>:     endbr64 
<+4>:     push   rbp
<+5>:     mov    rbp,rsp
<+8>:     mov    DWORD PTR [rbp-0x14],edi
<+11>:    mov    QWORD PTR [rbp-0x20],rsi
<+15>:    mov    DWORD PTR [rbp-0xc],0x9fe1a
<+22>:    mov    DWORD PTR [rbp-0x8],0x4
<+29>:    mov    eax,DWORD PTR [rbp-0xc]
<+32>:    imul   eax,DWORD PTR [rbp-0x8]
<+36>:    add    eax,0x1f5
<+41>:    mov    DWORD PTR [rbp-0x4],eax
<+44>:    mov    eax,DWORD PTR [rbp-0x4]
<+47>:    pop    rbp
<+48>:    ret
```
- Al analizar el código esto es lo que ejecuta el CPU.
```bash
<+15>: Se almacena el valor DWORD 654874 en la ubicación de memoria apuntada por [rbp-0xc].
<+22>: Se almacena el valor DWORD 4 en la ubicación de memoria apuntada por [rbp-0x8].
<+29>: El valor almacenado en la ubicación de memoria apuntada por [rbp-0xc](654874) se almacena en el registro eax.
<+32>: El valor almacenado en el registro eax se multiplica con el valor almacenado en la ubicación de memoria apuntada por [rbp-0x8] (4) y el resultado se almacena en el registro eax.
<+36>: El valor 501 se suma al valor almacenado en el registro eax y el resultado se almacena en el registro eax.
<+41>: El valor almacenado en el registro eax se almacena en la ubicación de memoria apuntada por [rbp-0x4].
<+44>: El valor en la ubicación de memoria apuntada por [rbp-0x4] se almacena en el registro eax.
```
- Realizamos las operaciones que se hacen para obtener el valor final de `eax`.
```bash
┌──(armando㉿kali)-[~/picoCTF/reversing/Bit-O-Asm-3]
└─$ python3
Python 3.12.6 (main, Sep  7 2024, 14:20:15) [GCC 14.2.0] on linux
Type "help", "copyright", "credits" or "license" for more information.
>>> (0x9fe1a * 0x4) + 0x1f5
2619997
>>> 

┌──(armando㉿kali)-[~/picoCTF/reversing/Bit-O-Asm-3]
└─$ 
```
- Por lo tanto la bandera quedaría de la siguiente forma.
```bash
picoCTF{2619997}
```

## Notas Adicionales
## Referencias