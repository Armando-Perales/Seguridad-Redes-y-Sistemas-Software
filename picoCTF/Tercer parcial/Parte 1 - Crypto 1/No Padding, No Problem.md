## Objetivo
Oracles can be your best friend, they will decrypt anything, except the flag's ciphertext. How will you break it? Connect with `nc mercury.picoctf.net 10333`.
## Solución

```bash
┌──(armando㉿kali)-[~/picoCTF/crypto/NoPaddingNoProblem]
└─$ nc mercury.picoctf.net 10333
Welcome to the Padding Oracle Challenge
This oracle will take anything you give it and decrypt using RSA. It will not accept the ciphertext with the secret message... Good Luck!


n: 110953126107626175879965128686935482184506053700881171548007554478916770274846705808470989693545045436097823497801374361331172638486106053607181090237987044865529548463323051520040210730996825219132814348770763144076159956701939679636654076079845581840724300002178625491930656128398736599814110329265416542489
e: 65537
ciphertext: 16265255073209594261948411679654171847492629850898842710456645431356039180995119622202630468161283990462904986519656961229623546022069066267733911746433410889392413881888257105933687078270331619497695371850410497722942790192332539819966404297336565219485046547754756927282205716537351882242098722492707632223


Give me ciphertext to decrypt: 16265255073209594261948411679654171847492629850898842710456645431356039180995119622202630468161283990462904986519656961229623546022069066267733911746433410889392413881888257105933687078270331619497695371850410497722942790192332539819966404297336565219485046547754756927282205716537351882242098722492707632223
Will not decrypt the ciphertext. Try Again
Give me ciphertext to decrypt: ^C

┌──(armando㉿kali)-[~/picoCTF/crypto/NoPaddingNoProblem]
└─$ nano solve.py               
```
- Creamos un programa en Python para que obtenga la bandera.
```python
from pwn import *
import binascii

r = remote('mercury.picoctf.net', 10333)
r.recvlines(4)

r.recvuntil(b'n: ')
n = int(r.recvline().strip())

r.recvuntil(b'e: ')
e = int(r.recvline().strip())

r.recvuntil(b'ciphertext: ')
c = int(r.recvline().strip())

payload = c * pow(2,e,n)
r.sendlineafter(b'Give me ciphertext to decrypt: ', str(payload))

r.recvuntil(b'Here you go: ')
doubled_plain = int(r.recvline().strip())
print("Doubled Plain:", doubled_plain)

plain_hex = hex(doubled_plain // 2)[2:]
plain_bytes = bytes.fromhex(plain_hex)
print("Plain Text Hex:", plain_hex)
print("Plain Text:", plain_bytes.decode())

r.close()
```
- Ejecutamos el programa y obtendremos la bandera.
```bash
┌──(armando㉿kali)-[~/picoCTF/crypto/NoPaddingNoProblem]
└─$ python3 solve.py            
[+] Opening connection to mercury.picoctf.net on port 10333: Done
/home/armando/picoCTF/crypto/NoPaddingNoProblem/solve.py:17: BytesWarning: Text is not bytes; assuming ASCII, no guarantees. See https://docs.pwntools.com/#bytes
  r.sendlineafter(b'Give me ciphertext to decrypt: ', str(payload))
Doubled Plain: 580550060391700078946913236734911770139931497702556153513487440893406629034802718534645538074938502890768853279675297196794
Plain Text Hex: 7069636f4354467b6d347962335f54683073655f6d337335346733735f3472335f646966757272656e745f313737323733357d
Plain Text: picoCTF{m4yb3_Th0se_m3s54g3s_4r3_difurrent_1772735}
[*] Closed connection to mercury.picoctf.net port 10333

┌──(armando㉿kali)-[~/picoCTF/crypto/NoPaddingNoProblem]
└─$ 
```

## Notas Adicionales
## Referencias
- [Homomorphic encryption](https://en.wikipedia.org/wiki/Homomorphic_encryption)