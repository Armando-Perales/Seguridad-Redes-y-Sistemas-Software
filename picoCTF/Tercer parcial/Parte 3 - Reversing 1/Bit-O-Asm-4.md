## Objetivo
Can you figure out what is in the `eax` register? Put your answer in the picoCTF flag format: `picoCTF{n}` where `n` is the contents of the `eax` register in the decimal number base. If the answer was `0x11` your flag would be `picoCTF{17}`. Download the assembly dump [here](https://artifacts.picoctf.net/c/511/disassembler-dump0_d.txt).
## Solución

```bash
┌──(armando㉿kali)-[~/picoCTF/reversing/Bit-O-Asm-4]
└─$ ls
disassembler-dump0_d.txt

┌──(armando㉿kali)-[~/picoCTF/reversing/Bit-O-Asm-4]
└─$ file disassembler-dump0_d.txt 
disassembler-dump0_d.txt: ASCII text

┌──(armando㉿kali)-[~/picoCTF/reversing/Bit-O-Asm-4]
└─$ cat disassembler-dump0_d.txt 
<+0>:     endbr64 
<+4>:     push   rbp
<+5>:     mov    rbp,rsp
<+8>:     mov    DWORD PTR [rbp-0x14],edi
<+11>:    mov    QWORD PTR [rbp-0x20],rsi
<+15>:    mov    DWORD PTR [rbp-0x4],0x9fe1a
<+22>:    cmp    DWORD PTR [rbp-0x4],0x2710
<+29>:    jle    0x55555555514e <main+37>
<+31>:    sub    DWORD PTR [rbp-0x4],0x65
<+35>:    jmp    0x555555555152 <main+41>
<+37>:    add    DWORD PTR [rbp-0x4],0x65
<+41>:    mov    eax,DWORD PTR [rbp-0x4]
<+44>:    pop    rbp
<+45>:    ret
```
- Al analizar el código esto es lo que ejecuta el CPU.
```bash
<+15>: Almacena 0x9fe1a en la ubicación de memoria apuntada por [rbp-0x4].
<+22>: Compara [rbp-0x4] con 0x2710.
<+29>: Salta a la instrucción en <+37> si [rbp-0x4] es menor o igual a 0x2710 (NO lo es).
<+31>: Resta 0x65 de [rbp-0x4] y almacenar el resultado en [rbp-0x4].
<+35>: Salta a <+41>.
<+37>: [NO EJECUTADO].
<+41>: Almacena el valor apuntado por [rbp-0x4] en el registro eax.
```
- Realizamos las operaciones que se hacen para obtener el valor final de `eax`.
```bash
┌──(armando㉿kali)-[~/picoCTF/reversing/Bit-O-Asm-4]
└─$ python3
Python 3.12.6 (main, Sep  7 2024, 14:20:15) [GCC 14.2.0] on linux
Type "help", "copyright", "credits" or "license" for more information.
>>> 0x9fe1a
654874
>>> 0x2710
10000
>>> 0x9fe1a - 0x65
654773
>>> 

┌──(armando㉿kali)-[~/picoCTF/reversing/Bit-O-Asm-4]
└─$ 
```
- Por lo tanto la bandera quedaría de la siguiente forma.
```bash
picoCTF{654773}
```

## Notas Adicionales
## Referencias