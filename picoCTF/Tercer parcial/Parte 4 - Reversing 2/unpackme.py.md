## Objetivo
Can you get the flag? Reverse engineer this [Python program](https://artifacts.picoctf.net/c/49/unpackme.flag.py).
## Solución

```bash
┌──(armando㉿kali)-[~/picoCTF/reversing/unpackme.py]
└─$ ls
unpackme.flag.py

┌──(armando㉿kali)-[~/picoCTF/reversing/unpackme.py]
└─$ nano unpackme.flag.py 
```
- Revisamos el programa que nos dan.
```python
import base64
from cryptography.fernet import Fernet



payload = b'gAAAAABkzWGSzE6VQNTzvRXOXekQeW4CY6NiRkzeImo9LuYBHAYw_hagTJLJL0c-kmNsjY33IUbU2IWlqxA3Fpp9S7RxNkiwMDZgLmRlI9-lGAEW-_i72RSDvylNR3QkpJW2JxubjLUC5VwoVgH62wxDuYu1rRD5KadwTADdABqsx2MkY6fKNTMCYY09Se6yjtRBftfTJUL-LKz2bwgXNd6O-WpbfXEMvCv3gNQ7sW4pgUnb-gDVZvrLNrug_1YFaIe3yKr0Awo0HIN3XMdZYpSE1c9P4G0sMQ=='

key_str = 'correctstaplecorrectstaplecorrec'
key_base64 = base64.b64encode(key_str.encode())
f = Fernet(key_base64)
plain = f.decrypt(payload)
exec(plain.decode())
```
- Podemos ver un `payload` (aparentemente codificado en base64), que será descifrado usando la variable `key_str`, que a su vez está codificada en base64.
- Después de esto, el `payload` decodificado será ejecutado, por lo que posiblemente, el `payload` en sí es un pequeño programa.
- Y esto lo podemos confirmar si intentamos ejecutar el programa.
```bash
┌──(armando㉿kali)-[~/picoCTF/reversing/unpackme.py]
└─$ python3 unpackme.flag.py 
What's the password? z
That password is incorrect.

┌──(armando㉿kali)-[~/picoCTF/reversing/unpackme.py]
└─$ nano unpackme.flag.py
```
- Regresando al código si le hacemos una ligera modificación para imprimir la carga útil decodificada.
```python
import base64
from cryptography.fernet import Fernet



payload = b'gAAAAABkzWGSzE6VQNTzvRXOXekQeW4CY6NiRkzeImo9LuYBHAYw_hagTJLJL0c-kmNsjY33IUbU2IWlqxA3Fpp9S7RxNkiwMDZgLmRlI9-lGAEW-_i72RSDvylNR3QkpJW2JxubjLUC5VwoVgH62wxDuYu1rRD5KadwTADdABqsx2MkY6fKNTMCYY09Se6yjtRBftfTJUL-LKz2bwgXNd6O-WpbfXEMvCv3gNQ7sW4pgUnb-gDVZvrLNrug_1YFaIe3yKr0Awo0HIN3XMdZYpSE1c9P4G0sMQ=='

key_str = 'correctstaplecorrectstaplecorrec'
key_base64 = base64.b64encode(key_str.encode())
f = Fernet(key_base64)
plain = f.decrypt(payload)

print(plain)
#exec(plain.decode())
```
- Tal como se esperaba, la carga útil es un script de Python, y nuestra bandera también se encuentra ahí para tomarla.
```
┌──(armando㉿kali)-[~/picoCTF/reversing/unpackme.py]
└─$ python3 unpackme.flag.py
b"\npw = input('What\\'s the password? ')\n\nif pw == 'batteryhorse':\n  print('picoCTF{175_chr157m45_cd82f94c}')\nelse:\n  print('That password is incorrect.')\n\n"

┌──(armando㉿kali)-[~/picoCTF/reversing/unpackme.py]
└─$ 
```

## Notas Adicionales
## Referencias