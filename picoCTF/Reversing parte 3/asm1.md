## Objetivo
What does asm1(0x6fa) return? Submit the flag as a hexadecimal value (starting with '0x'). NOTE: Your submission for this question will NOT be in the normal flag format. [Source](https://jupiter.challenges.picoctf.org/static/b41e08fc19ceb9d0466ebd68d36c5630/test.S)
## Solución

```bash
┌──(armando㉿kali)-[~/picoCTF/reversing/asm1]
└─$ ls
test.S

┌──(armando㉿kali)-[~/picoCTF/reversing/asm1]
└─$ nano test.S     
```

```
asm1:
        <+0>:   push   ebp
        <+1>:   mov    ebp,esp
        <+3>:   cmp    DWORD PTR [ebp+0x8],0x3a2
        <+10>:  jg     0x512 <asm1+37>
        <+12>:  cmp    DWORD PTR [ebp+0x8],0x358
        <+19>:  jne    0x50a <asm1+29>
        <+21>:  mov    eax,DWORD PTR [ebp+0x8]
        <+24>:  add    eax,0x12
        <+27>:  jmp    0x529 <asm1+60>
        <+29>:  mov    eax,DWORD PTR [ebp+0x8]
        <+32>:  sub    eax,0x12
        <+35>:  jmp    0x529 <asm1+60>
        <+37>:  cmp    DWORD PTR [ebp+0x8],0x6fa
        <+44>:  jne    0x523 <asm1+54>
        <+46>:  mov    eax,DWORD PTR [ebp+0x8]
        <+49>:  sub    eax,0x12
        <+52>:  jmp    0x529 <asm1+60>
        <+54>:  mov    eax,DWORD PTR [ebp+0x8]
        <+57>:  add    eax,0x12
        <+60>:  pop    ebp
        <+61>:  ret    
```
- Ejecutamos el programa a mano y con ayuda de `Python` vamos realizando las comparaciones y así nos vamos hasta llegar al ultimo paso del programa.
```bash
stack
00000




[ebp  ] < ebp < esp
[ret  ] ebp + 0x4
[0x6fa] ebp + 0x8
fffff

Registers
[0x6e8] eax


asm1(0x6fa):
        <+0>:   push   ebp
        <+1>:   mov    ebp,esp

        <+3>:   cmp    DWORD PTR [ebp+0x8],0x3a2
        <+10>:  jg     0x512 <asm1+37>
        <+12>:  cmp    DWORD PTR [ebp+0x8],0x358
        <+19>:  jne    0x50a <asm1+29>
        <+21>:  mov    eax,DWORD PTR [ebp+0x8]
        <+24>:  add    eax,0x12
        <+27>:  jmp    0x529 <asm1+60>
        <+29>:  mov    eax,DWORD PTR [ebp+0x8]
        <+32>:  sub    eax,0x12
        <+35>:  jmp    0x529 <asm1+60>
..      <+37>:  cmp    DWORD PTR [ebp+0x8],0x6fa
        <+44>:  jne    0x523 <asm1+54>
        <+46>:  mov    eax,DWORD PTR [ebp+0x8]
        <+49>:  sub    eax,0x12
        <+52>:  jmp    0x529 <asm1+60>
        <+54>:  mov    eax,DWORD PTR [ebp+0x8]
        <+57>:  add    eax,0x12
        <+60>:  pop    ebp
        <+61>:  ret    

```

```
┌──(armando㉿kali)-[~/picoCTF/reversing/asm1]
└─$ python3
Python 3.12.6 (main, Sep  7 2024, 14:20:15) [GCC 14.2.0] on linux
Type "help", "copyright", "credits" or "license" for more information.
>>> 0x6fa > 0x3a2
True
>>> 0x6fa != 0x6fa
False
>>> hex(0x6fa - 0x12)
'0x6e8'
>>> 
```

```bash
0x6e8
```

## Notas Adicionales
## Referencias
- [x86 Assembly Guide](https://www.google.com/url?sa=t&source=web&rct=j&opi=89978449&url=https://www.cs.virginia.edu/~evans/cs216/guides/x86.html&ved=2ahUKEwiBy-qVj8OJAxWZHkQIHR9CD88QFnoECBoQAQ&usg=AOvVaw0IXe1d-9ViADmhhLTOpLi2)