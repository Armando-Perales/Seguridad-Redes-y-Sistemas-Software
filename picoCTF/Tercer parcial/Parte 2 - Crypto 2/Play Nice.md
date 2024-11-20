## Objetivo
Not all ancient ciphers were so bad... The flag is not in standard format. `nc mercury.picoctf.net 30568` [playfair.py](https://mercury.picoctf.net/static/9e655bebf3ad245e74ce5ca3a8352af1/playfair.py)
## Solución
- Observamos que nos dan un alfabeto y un mensaje encriptado.
```bash
┌──(armando㉿kali)-[~/picoCTF/crypto/PlayNice]
└─$ ls
playfair.py

┌──(armando㉿kali)-[~/picoCTF/crypto/PlayNice]
└─$ nc mercury.picoctf.net 30568
Here is the alphabet: 0fkdwu6rp8zvsnlj3iytxmeh72ca9bg5o41q
Here is the encrypted message: herfayo7oqxrz7jwxx15ie20p40u1i
What is the plaintext message? 

┌──(armando㉿kali)-[~/picoCTF/crypto/PlayNice]
└─$ nano playfair.py     
```
- Revisamos el programa que nos dan.
```python
#!/usr/bin/python3 -u
import signal

SQUARE_SIZE = 6


def generate_square(alphabet):
        assert len(alphabet) == pow(SQUARE_SIZE, 2)
        matrix = []
        for i, letter in enumerate(alphabet):
                if i % SQUARE_SIZE == 0:
                        row = []
                row.append(letter)
                if i % SQUARE_SIZE == (SQUARE_SIZE - 1):
                        matrix.append(row)
        return matrix

def get_index(letter, matrix):
        for row in range(SQUARE_SIZE):
                for col in range(SQUARE_SIZE):
                        if matrix[row][col] == letter:
                                return (row, col)
        print("letter not found in matrix.")
        exit()

def encrypt_pair(pair, matrix):
        p1 = get_index(pair[0], matrix)
        p2 = get_index(pair[1], matrix)

        if p1[0] == p2[0]:
                return matrix[p1[0]][(p1[1] + 1)  % SQUARE_SIZE] + matrix[p2[0]][(p2[1] + 1)  % SQUARE_SIZE]
        elif p1[1] == p2[1]:
                return matrix[(p1[0] + 1)  % SQUARE_SIZE][p1[1]] + matrix[(p2[0] + 1)  % SQUARE_SIZE][p2[1]]
        else:
                return matrix[p1[0]][p2[1]] + matrix[p2[0]][p1[1]]

def encrypt_string(s, matrix):
        result = ""
        if len(s) % 2 == 0:
                plain = s
        else:
                plain = s + "0fkdwu6rp8zvsnlj3iytxmeh72ca9bg5o41q"[0]
        for i in range(0, len(plain), 2):
                result += encrypt_pair(plain[i:i + 2], matrix)
        return result

alphabet = open("key").read().rstrip()
m = generate_square(alphabet)
msg = open("msg").read().rstrip()
enc_msg = encrypt_string(msg, m)
print("Here is the alphabet: {}\nHere is the encrypted message: {}".format(alphabet, enc_msg))
signal.alarm(18)
resp = input("What is the plaintext message? ").rstrip()
if resp and resp == msg:
        print("Congratulations! Here's the flag: {}".format(open("flag").read()))

# https://en.wikipedia.org/wiki/Playfair_cipher
```
```bash
┌──(armando㉿kali)-[~/picoCTF/crypto/PlayNice]
└─$ nano solve.py   
```
- Creamos un programa para que descifre el texto.
```python
SQUARE_SIZE = 6
def generate_square(alphabet):
        assert len(alphabet) == pow(SQUARE_SIZE, 2) #can be ignored here
        matrix = []
        for i, letter in enumerate(alphabet):
                if i % SQUARE_SIZE == 0: #i%6==0
                        row = []
                row.append(letter)
                if i % SQUARE_SIZE == (SQUARE_SIZE - 1):
                        matrix.append(row)
        return matrix

def get_index(letter, matrix):
        for row in range(SQUARE_SIZE):
                for col in range(SQUARE_SIZE):
                        if matrix[row][col] == letter:
                                return (row, col)
        print("letter not found in matrix.")
        exit()

def decrypt_pair(pair, matrix):
        #print("pair=",pair)
        p1 = get_index(pair[0], matrix) #(row,col)
        p2 = get_index(pair[1], matrix) #(row,col)

        if p1[0] == p2[0]: #same row
                return matrix[p1[0]][(p1[1] - 1)  % SQUARE_SIZE] + matrix[p2[0]][(p2[1] - 1)  % SQUARE_SIZE]
        elif p1[1] == p2[1]: #same col
                return matrix[(p1[0] - 1)  % SQUARE_SIZE][p1[1]] + matrix[(p2[0] - 1)  % SQUARE_SIZE][p2[1]]
        else: #neither
                return matrix[p1[0]][p2[1]] + matrix[p2[0]][p1[1]]

def decrypt_string(s, matrix):
        result = ""
        for i in range(0, len(s), 2):
                print("now i=",i)
                result += decrypt_pair(s[i:i + 2], matrix)
        return result

alphabet = "0fkdwu6rp8zvsnlj3iytxmeh72ca9bg5o41q"
m = generate_square(alphabet) #key table
enc_msg="herfayo7oqxrz7jwxx15ie20p40u1i"
msg=decrypt_string(enc_msg,m)
print(msg)
```
- Ejecutamos el programa y el texto generado se lo enviamos como solución.
```bash
┌──(armando㉿kali)-[~/picoCTF/crypto/PlayNice]
└─$ python3 solve.py        
now i= 0
now i= 2
now i= 4
now i= 6
now i= 8
now i= 10
now i= 12
now i= 14
now i= 16
now i= 18
now i= 20
now i= 22
now i= 24
now i= 26
now i= 28
emf57mgc51tp693dtt4g3h7f8ouwq3

┌──(armando㉿kali)-[~/picoCTF/crypto/PlayNice]
└─$ nc mercury.picoctf.net 30568
Here is the alphabet: 0fkdwu6rp8zvsnlj3iytxmeh72ca9bg5o41q
Here is the encrypted message: herfayo7oqxrz7jwxx15ie20p40u1i
What is the plaintext message? emf57mgc51tp693dtt4g3h7f8ouwq3
Congratulations! Here's the flag: 007d0a696aaad7fb5ec21c7698e4f754

┌──(armando㉿kali)-[~/picoCTF/crypto/PlayNice]
└─$
```

```bash
007d0a696aaad7fb5ec21c7698e4f754
```

## Notas Adicionales
## Referencias
