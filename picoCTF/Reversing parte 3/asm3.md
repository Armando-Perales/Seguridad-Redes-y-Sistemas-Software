## Objetivo
asm3(0xba6c5a02,0xd101e3dd,0xbb86a173) return? Submit the flag as a hexadecimal value (starting with '0x'). NOTE: Your submission for this question will NOT be in the normal flag format. [Source](https://jupiter.challenges.picoctf.org/static/cb753ae52bca4aa303deca5fbfb01bfb/test.S)
## Solución

```bash
┌──(armando㉿kali)-[~/picoCTF/reversing/asm2/asm3]
└─$ ls    
test.S

┌──(armando㉿kali)-[~/picoCTF/reversing/asm2/asm3]
└─$ nano test.S 
```

```bash
asm3:
        <+0>:   push   ebp
        <+1>:   mov    ebp,esp
        <+3>:   xor    eax,eax
        <+5>:   mov    ah,BYTE PTR [ebp+0xb]
        <+8>:   shl    ax,0x10
        <+12>:  sub    al,BYTE PTR [ebp+0xd]
        <+15>:  add    ah,BYTE PTR [ebp+0xc]
        <+18>:  xor    ax,WORD PTR [ebp+0x12]
        <+22>:  nop
        <+23>:  pop    ebp
        <+24>:  ret 
```
- Entramos a un página que es un emulador para el lenguaje maquina, colocamos el código, abrimos la ventana que nos muestra los registros con forme al progreso de la ejecución del programa y ya solo nos fuimos moviendo paso a paso hasta llegar al ultimo paso y la bandera se encuentra en la variable `EAX`.
![[20241104114758.png]]

```bash
0x669B
```

## Notas Adicionales
## Referencias
- [Assembly x86 Emulator](https://www.google.com/url?sa=t&source=web&rct=j&opi=89978449&url=https://carlosrafaelgn.com.br/Asm86/&ved=2ahUKEwiliMrcnsOJAxV_J0QIHV2dHMIQFnoECBgQAQ&usg=AOvVaw1I3gydyd1l-jydi5eF2iBR)