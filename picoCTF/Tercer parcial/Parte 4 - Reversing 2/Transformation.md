## Objetivo
I wonder what this really is... [enc](https://mercury.picoctf.net/static/77a2b202236aa741e988581e78d277a6/enc) `''.join([chr((ord(flag[i]) << 8) + ord(flag[i + 1])) for i in range(0, len(flag), 2)])`
## Solución

```bash
┌──(armando㉿kali)-[~/picoCTF/reversing/Transformation]
└─$ cat enc          
灩捯䍔䙻ㄶ形楴獟楮獴㌴摟潦弸強㕤㐸㤸扽                                                                                                                    
┌──(armando㉿kali)-[~/picoCTF/reversing/Transformation]
└─$ nano solve.py
```
- Creamos un programa en Python para que decodifique la bandera.
```python
encoded_flag = open("enc").read()
flag = ""
for i in range(0, len(encoded_flag)):
    character1 = chr((ord(encoded_flag[i]) >> 8))
    character2 = chr(encoded_flag[i].encode('utf-16be')[-1])
    flag += character1
    flag += character2

print("Flag: " + flag)
```
- Ejecutamos el programa que creamos.
```bash
┌──(armando㉿kali)-[~/picoCTF/reversing/Transformation]
└─$ python3 solve.py
Flag: picoCTF{16_bits_inst34d_of_8_75d4898b}

┌──(armando㉿kali)-[~/picoCTF/reversing/Transformation]
└─$ 
```

## Notas Adicionales
## Referencias