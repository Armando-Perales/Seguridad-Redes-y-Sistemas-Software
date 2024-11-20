## Objetivo
We found a brand new type of encryption, can you break the secret code? (Wrap with picoCTF{}) `lkmjkemjmkiekeijiiigljlhilihliikiliginliljimiklligljiflhiniiiniiihlhilimlhijil` [new_caesar.py](https://mercury.picoctf.net/static/c9043977604318594ab73d126a01d0b1/new_caesar.py)
## Solución

```bash
┌──(armando㉿kali)-[~/picoCTF/crypto/NewCaesar]
└─$ ls
new_caesar.py

┌──(armando㉿kali)-[~/picoCTF/crypto/NewCaesar]
└─$ nano new_caesar.py        
```
- Revisamos el código que encripto la bandera.
```python
import string

LOWERCASE_OFFSET = ord("a")
ALPHABET = string.ascii_lowercase[:16]

def b16_encode(plain):
        enc = ""
        for c in plain:
                binary = "{0:08b}".format(ord(c))
                enc += ALPHABET[int(binary[:4], 2)]
                enc += ALPHABET[int(binary[4:], 2)]
        return enc

def shift(c, k):
        t1 = ord(c) - LOWERCASE_OFFSET
        t2 = ord(k) - LOWERCASE_OFFSET
        return ALPHABET[(t1 + t2) % len(ALPHABET)]

flag = "redacted"
key = "redacted"
assert all([k in ALPHABET for k in key])
assert len(key) == 1

b16 = b16_encode(flag)
enc = ""
for i, c in enumerate(b16):
        enc += shift(c, key[i % len(key)])
print(enc)
```
- Creamos un programa en Python que desencripté el texto que nos dieron.
```bash
┌──(armando㉿kali)-[~/picoCTF/crypto/NewCaesar]
└─$ nano solve.py     
```
```python
import string

LOWERCASE_OFFSET = ord("a")
ALPHABET = string.ascii_lowercase[:16]

def b16_decode(cipher):
    dec = ""
    for c in range(0, len(cipher), 2):
        b = ""
        b += "{0:04b}".format(ALPHABET.index(cipher[c]))
        b += "{0:04b}".format(ALPHABET.index(cipher[c + 1]))
        dec += chr(int(b, 2))
    return dec

def unshift(c, k):
    t1 = ord(c) - LOWERCASE_OFFSET
    t2 = ord(k) - LOWERCASE_OFFSET
    return ALPHABET[(t1 - t2) % len(ALPHABET)]

enc = "lkmjkemjmkiekeijiiigljlhilihliikiliginliljimiklligljiflhiniiiniiihlhilimlhijil"

for key in ALPHABET:
    s = ""
    for i, c in enumerate(enc):
        s += unshift(c, key[i % len(key)])
    s = b16_decode(s)
    print(s)
```
- Ejecutamos el programa.
```bash
┌──(armando㉿kali)-[~/picoCTF/crypto/NewCaesar]
└─$ python3 solve.py 
ºÉ¤ÉÊ¤¹·¸¸¹»¹···
©¸¸¹sxwu¨¦zv§yzu|§¨{yªu¨t¦|w|wv¦z{¦xz
§§¨bgfdiehidkjhdckfkfeijgi
qQqVUSXTWXSZYWSRZUZUTXYVX
v`@`EDBusGCtFGBItuHFwBuAsIDIDCsGHsEG
et_tu?_431db62c5618cd75f1d0b83832b67b46
TcNcd.N#" SQ%!R$% 'RS&$U S/Q'"'"!Q%&Q#%
CR=RS=B@AABDB@@@
2A,AB
???  ,1?00131
!01ûÿý .òþ/ñòýô/ óñ"ý ü.ôÿôÿþ.òó.ðò
/
/ ê
ïîìáíàáìãâàìëãîãîíáâïá
ùÙùÞÝÛ
ÑßÛÚ  ÐÜ
    ÒÝÒÝÜ
         ÐÑ
           ÞÐ
ÈèÍÌÊýûÏËüÎÏÊÁüýÀÎÿÊýÉûÁÌÁÌËûÏÀûÍÏ
íü×üý·×¼»¹ìê¾ºë½¾¹°ëì¿½î¹ì¸ê°»°»ºê¾¿ê¼¾
ÜëÆëì¦Æ«ª¨ÛÙ­©Ú¬­¨¯ÚÛ®¬Ý¨Û§Ù¯ª¯ª©Ù­®Ù«­
ËÚµÚÛµÊÈÉÉÊÊÈÈÈ

┌──(armando㉿kali)-[~/picoCTF/crypto/NewCaesar]
└─$ 
```
- Buscamos el texto y le aplicamos el formato de la bandera.
```bash
picoCTF{et_tu?_431db62c5618cd75f1d0b83832b67b46}
```

## Notas Adicionales
## Referencias