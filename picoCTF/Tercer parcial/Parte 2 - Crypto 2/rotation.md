## Objetivo
You will find the flag after decrypting this file Download the encrypted flag [here](https://artifacts.picoctf.net/c/388/encrypted.txt).
## Solución
- Nos dan un archivo `txt` con la bandera rotada.
```bash
┌──(armando㉿kali)-[~/picoCTF/crypto/rotation]
└─$ ls
encrypted.txt

┌──(armando㉿kali)-[~/picoCTF/crypto/rotation]
└─$ cat encrypted.txt   
xqkwKBN{z0bib1wv_l3kzgxb3l_25l7k61j}

┌──(armando㉿kali)-[~/picoCTF/crypto/rotation]
└─$ 
```
- Abrimos `CyberChef` y lo rotamos hasta obtener la bandera.
![[20241117191921.png]]

## Notas Adicionales
## Referencias