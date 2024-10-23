## Objetivo
We found this weird message being passed around on the servers, we think we have a working decryption scheme.Download the message [here](https://artifacts.picoctf.net/c/128/message.txt).Take each number mod 37 and map it to the following character set: 0-25 is the alphabet (uppercase), 26-35 are the decimal digits, and 36 is an underscore.Wrap your decrypted message in the picoCTF flag format (i.e. `picoCTF{decrypted_message}`)
## Solución
- Creamos un código en `Python` que le sacara el modulo 37 a los números y dependiendo del resultado ver si es una letra, un número o un guión bajo. 
```bash
┌──(armando㉿kali)-[~/picoCTF/crypto/basicmod1]
└─$ ls
message.txt

┌──(armando㉿kali)-[~/picoCTF/crypto/basicmod1]
└─$ cat message.txt 
165 248 94 346 299 73 198 221 313 137 205 87 336 110 186 69 223 213 216 216 177 138                                                                                                                  
┌──(armando㉿kali)-[~/picoCTF/crypto/basicmod1]
└─$ nano exp.py
```

```python
data = open('message.txt','r').read().split()
flag = ''
for c in data:
        char = int(c) % 37
        if char>=0 and char<=25:
                s = chr(char+65)
        elif char>=26 and char<=35:
                s = chr(char+22)
        elif char==36:
                s = '_'
        flag += s
        print(s)
print(flag)
```
- Ejecutamos el código.
```bash
┌──(armando㉿kali)-[~/picoCTF/crypto/basicmod1]
└─$ python exp.py
R
0
U
N
D
_
N
_
R
0
U
N
D
_
B
6
B
2
5
5
3
1
R0UND_N_R0UND_B6B25531

┌──(armando㉿kali)-[~/picoCTF/crypto/basicmod1]
└─$ 
```
- Y ya solo le aplicamos el formato de la bandera al valor dado
```bash
picoCTF{R0UND_N_R0UND_B6B25531}
```

## Notas Adicionales
## Referencias