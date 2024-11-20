## Objetivo
I just recently learnt about the SRA public key cryptosystem... or wait, was it supposed to be RSA? Hmmm, I should probably check... Connect to the program on our server: `nc saturn.picoctf.net 64954` Download the program: [chal.py](https://artifacts.picoctf.net/c/293/chal.py)
## Solución

```bash
┌──(armando㉿kali)-[~/picoCTF/crypto/SRA]
└─$ ls
chal.py

┌──(armando㉿kali)-[~/picoCTF/crypto/SRA]
└─$ nano chal.py   
```
```python
from Crypto.Util.number import getPrime, inverse, bytes_to_long
from string import ascii_letters, digits
from random import choice

pride = "".join(choice(ascii_letters + digits) for _ in range(16))
gluttony = getPrime(128)
greed = getPrime(128)
lust = gluttony * greed
sloth = 65537
envy = inverse(sloth, (gluttony - 1) * (greed - 1))

anger = pow(bytes_to_long(pride.encode()), sloth, lust)

print(f"{anger = }")
print(f"{envy = }")

print("vainglory?")
vainglory = input("> ").strip()

if vainglory == pride:
    print("Conquered!")
    with open("/challenge/flag.txt") as f:
        print(f.read())
else:
    print("Hubris!")
```
- Se nos proporciona un texto cifrado y el valor de d, pero no se nos proporciona n. Sabiendo que e\*d mod (p-1)(q-1)=1, y que p y q son primos de 128 bits, obtenemos una lista potencial de valores p y q, y luego intentamos descifrar con cada n posible. El que sale como texto simple es correcto, y luego el programa nos da la bandera.
```bash
┌──(armando㉿kali)-[~/picoCTF/crypto/SRA]
└─$ python3 -m venv venv                                             

┌──(armando㉿kali)-[~/picoCTF/crypto/SRA]
└─$ source venv/bin/activate          

┌──(venv)─(armando㉿kali)-[~/picoCTF/crypto/SRA]
└─$ pip install primefac
Collecting primefac
  Downloading primefac-2.0.12-py3-none-any.whl.metadata (13 kB)
Downloading primefac-2.0.12-py3-none-any.whl (54 kB)
Installing collected packages: primefac
Successfully installed primefac-2.0.12

┌──(venv)─(armando㉿kali)-[~/picoCTF/crypto/SRA]
└─$ pip install sympy
Collecting sympy
  Downloading sympy-1.13.3-py3-none-any.whl.metadata (12 kB)
Collecting mpmath<1.4,>=1.1.0 (from sympy)
  Downloading mpmath-1.3.0-py3-none-any.whl.metadata (8.6 kB)
Downloading sympy-1.13.3-py3-none-any.whl (6.2 MB)
   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 6.2/6.2 MB 313.2 kB/s eta 0:00:00
Downloading mpmath-1.3.0-py3-none-any.whl (536 kB)
   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 536.2/536.2 kB 870.7 kB/s eta 0:00:00
Installing collected packages: mpmath, sympy
Successfully installed mpmath-1.3.0 sympy-1.13.3

┌──(venv)─(armando㉿kali)-[~/picoCTF/crypto/SRA]
└─$ pip install pycryptodome                                           
Collecting pycryptodome
  Downloading pycryptodome-3.21.0-cp36-abi3-manylinux_2_17_x86_64.manylinux2014_x86_64.whl.metadata (3.4 kB)
Downloading pycryptodome-3.21.0-cp36-abi3-manylinux_2_17_x86_64.manylinux2014_x86_64.whl (2.3 MB)
   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 2.3/2.3 MB 1.2 MB/s eta 0:00:00
Installing collected packages: pycryptodome
Successfully installed pycryptodome-3.21.0

┌──(venv)─(armando㉿kali)-[~/picoCTF/crypto/SRA]
└─$ pip install pwntools 
...
┌──(venv)─(armando㉿kali)-[~/picoCTF/crypto/SRA]
└─$ nano solve.py 
```
- Creamos el programa llamado `solve.py` para que resuelva el ejercicio.
- Este recibe un mensaje cifrado (`ciphertext`) y una clave privada parcial (`d`), y luego intenta factorizar n=p×qn = p \times qn=p×q utilizando divisores de d×e−1d \times e - 1d×e−1 para encontrar los primos ppp y qqq. Prueba diferentes combinaciones de factores como posibles valores de p−1p-1p−1 y q−1q-1q−1, y usa estos valores para descifrar el mensaje. Finalmente, si obtiene un descifrado legible, lo envía al servidor para completar el desafío.
```python
from pwn import *
import primefac
from itertools import combinations
from Crypto.Util.number import long_to_bytes

#function to generate all the sub lists
def sub_lists (l):
    #initializing empty list
    comb = []

    #Iterating till length of list
    for i in range(1,len(l)+1):
        #Generating sub list
        comb += [list(j) for j in combinations(l, i)]
    #Returning list
    return comb

def divisors(phi):
   print("Give me the divisors of ", phi-1)
   #this is dangerous, but I'm trusting me
   return(eval(input()))

#connect to the server
r = remote('saturn.picoctf.net', 64954)
#get ciphertext
r.recvuntil("anger =")
ciphertext=int(r.recvline())
#get d
r.recvuntil("envy =")
d=int(r.recvline())
print("cipher=",ciphertext)
print("d=",d)
print(r.recvuntil("vainglory?"))
r.recvline()
#since d is e^-1 mod (p-1)*(q-1), d*e=k*(p-1)*(q-1)+1
#so (p-1)*(q-1)*k = d*e-1
factors=divisors(d*65537)
combos = sub_lists(factors)
primes = set()
#try all possible subsets of the list of factors as the factors of (p-1)
for l in combos:
   product = 1
   #multiply them together to get p-1
   for k in l:
      product = product * k
   #if the right length and adding 1 yields a prime, then maybe
   if product.bit_length()==128 and primefac.isprime(product+1):
      primes.add(product+1)
print(primes)
primelist = list(primes)
#try all possible prime pairs
for p in primelist:
   for q in primelist:
      n=p*q
      #decode with this possible n
      plain = pow(ciphertext,d,n)
      try:
         plaintext = long_to_bytes(plain)
         #see if it corresponds to text and if so, try it
         print(plaintext.decode())
         r.sendline(plaintext.decode())
         print(r.recvline())
         print(r.recvline())
         print(r.recvline())
      except:
         continue
```
- Ejecutamos el código.
```bash
┌──(venv)─(armando㉿kali)-[~/picoCTF/crypto/SRA]
└─$ python3 solve.py
[+] Opening connection to saturn.picoctf.net on port 64954: Done
/home/armando/picoCTF/crypto/SRA/solve.py:26: BytesWarning: Text is not bytes; assuming ASCII, no guarantees. See https://docs.pwntools.com/#bytes
  r.recvuntil("anger =")
/home/armando/picoCTF/crypto/SRA/solve.py:29: BytesWarning: Text is not bytes; assuming ASCII, no guarantees. See https://docs.pwntools.com/#bytes
  r.recvuntil("envy =")
cipher= 9921021662909706801318607712464902266644794223098095065247413792050982713473
d= 11249115700854165359988414957041564704044996248825349318377043662200472495105
/home/armando/picoCTF/crypto/SRA/solve.py:33: BytesWarning: Text is not bytes; assuming ASCII, no guarantees. See https://docs.pwntools.com/#bytes
  print(r.recvuntil("vainglory?"))
b'vainglory?'
Give me the divisors of  737233295686879435197560751039633026008996919159266918278476310489632365911696384
[2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 3, 11, 19, 83, 269, 32941, 67489, 14043728143, 14344444803919, 2767345963330292161, 41496138548468820233]
{235756060292477447108497272495326427689, 181996582615747564659663469398395798837, 181639300868096232024109838788325803699, 170168355241195474384639175504796977857, 280118439892967683121518787528984371969}
MegVRMUizdziV5op
/home/armando/picoCTF/crypto/SRA/solve.py:61: BytesWarning: Text is not bytes; assuming ASCII, no guarantees. See https://docs.pwntools.com/#bytes
  r.sendline(plaintext.decode())
b'> MegVRMUizdziV5op\r\n'
b'Conquered!\r\n'
b'picoCTF{7h053_51n5_4r3_n0_m0r3_0795e891}\r\n'
MegVRMUizdziV5op
[*] Closed connection to saturn.picoctf.net port 64954

┌──(venv)─(armando㉿kali)-[~/picoCTF/crypto/SRA]
└─$ 
```

```bash
picoCTF{7h053_51n5_4r3_n0_m0r3_0795e891}
```

## Notas Adicionales
- Obtenemos los divisores de 737233295686879435197560751039633026008996919159266918278476310489632365911696384 en esta pagina: [Prime Factors Decomposition](https://www.dcode.fr/prime-factors-decomposition) y los ponemos en forma de lista.
## Referencias
- [Prime Factors Decomposition](https://www.dcode.fr/prime-factors-decomposition)