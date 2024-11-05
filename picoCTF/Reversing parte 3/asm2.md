## Objetivo
What does asm2(0xb,0x2e) return? Submit the flag as a hexadecimal value (starting with '0x'). NOTE: Your submission for this question will NOT be in the normal flag format. [Source](https://jupiter.challenges.picoctf.org/static/717467c8c8b4332ea5873ad8fe7b2dad/test.S)
## Solución

```bash
┌──(armando㉿kali)-[~/picoCTF/reversing/asm2]
└─$ ls
test.S

┌──(armando㉿kali)-[~/picoCTF/reversing/asm2]
└─$ nano test.S 
```

```bash
asm2:
        <+0>:   push   ebp
        <+1>:   mov    ebp,esp
        <+3>:   sub    esp,0x10
        <+6>:   mov    eax,DWORD PTR [ebp+0xc]
        <+9>:   mov    DWORD PTR [ebp-0x4],eax
        <+12>:  mov    eax,DWORD PTR [ebp+0x8]
        <+15>:  mov    DWORD PTR [ebp-0x8],eax
        <+18>:  jmp    0x509 <asm2+28>
        <+20>:  add    DWORD PTR [ebp-0x4],0x1
        <+24>:  sub    DWORD PTR [ebp-0x8],0xffffff80
        <+28>:  cmp    DWORD PTR [ebp-0x8],0x63f3
        <+35>:  jle    0x501 <asm2+20>
        <+37>:  mov    eax,DWORD PTR [ebp-0x4]
        <+40>:  leave  
        <+41>:  ret    
```

```bash
┌──(armando㉿kali)-[~/picoCTF/reversing/asm2]
└─$ cat test.S 
[    ] < esp
[    ] ebp - 0xc
[0x8b] ebp - 0x8
[0x2f] ebp - 0x4
[ebp ] < ebp
[ret ] ebp + 0x4
[0xb ] ebp + 0x8
[0x2e] ebp + 0xc

[0xb ] eax

asm2(0xb,0x2e):
        <+0>:   push   ebp
        <+1>:   mov    ebp,esp

        <+3>:   sub    esp,0x10
        <+6>:   mov    eax,DWORD PTR [ebp+0xc]
        <+9>:   mov    DWORD PTR [ebp-0x4],eax
        <+12>:  mov    eax,DWORD PTR [ebp+0x8]
        <+15>:  mov    DWORD PTR [ebp-0x8],eax
        <+18>:  jmp    0x509 <asm2+28>
..      <+20>:  add    DWORD PTR [ebp-0x4],0x1
        <+24>:  sub    DWORD PTR [ebp-0x8],0xffffff80
        <+28>:  cmp    DWORD PTR [ebp-0x8],0x63f3
        <+35>:  jle    0x501 <asm2+20>
        <+37>:  mov    eax,DWORD PTR [ebp-0x4]

        <+40>:  leave  
        <+41>:  ret    

┌──(armando㉿kali)-[~/picoCTF/reversing/asm2]
└─$ 
```

```bash
┌──(armando㉿kali)-[~/picoCTF/reversing/asm2]
└─$ python3
Python 3.12.6 (main, Sep  7 2024, 14:20:15) [GCC 14.2.0]
Type "help", "copyright", "credits" or "license" for mor
>>> 0xb <= 0x63f3
True
>>> hex(0x2e + 0x1)
'0x2f'
>>> 0xb - 0xffffff80
-4294967157
>>> hex(0xb+128)
'0x8b'                                                  
>>> 0x8b <= 0x63f3                                      
True                                                    
>>>
```
- Obtenemos el número de veces que el programa tiene que hacer el ciclo para poder salirse, a ese valor le sumamos el valor entero de `0xb` y a eso le sumamos el número de las vueltas que obtuvimos y ya solo lo convertimos a hexadecimal.
```bash
>>> import numpy
>>> numpy.int32(0xffffff80)
<stdin>:1: DeprecationWarning: NumPy will stop allowing conversion of out-of-bound Python integers to integer arrays.  The conversion of 4294967168 to int32 will fail in the future.
For the old behavior, usually:
    np.array(value).astype(dtype)
will give the desired result (the cast overflows).
-128
>>> 0x63f3 / 128
199.8984375
>>> int(0xb)
11
>>> hex(246)
'0xf6'
>>> 
```

```bash
0xf6
```


## Notas Adicionales
## Referencias