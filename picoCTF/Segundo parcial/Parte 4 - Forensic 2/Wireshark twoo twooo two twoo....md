## Objetivo
Can you find the flag? [shark2.pcapng](https://mercury.picoctf.net/static/0fe13a33318e756f71c35cb490e64c81/shark2.pcapng).
## Solución
```bash
┌──(armando㉿kali)-[~/picoCTF/forensic/wiresharktwootwoootwotwoo]
└─$ ls
shark2.pcapng

┌──(armando㉿kali)-[~/picoCTF/forensic/wiresharktwootwoootwotwoo]
└─$ file shark2.pcapng 
shark2.pcapng: pcapng capture file - version 1.0
```
- Abrimos el archivo con `Wireshark`, filtramos los archivos que tienen como destino el puerto `18.217.1.57`.
```bash
┌──(armando㉿kali)-[~/picoCTF/forensic/wiresharktwootwoootwotwoo]
└─$ wireshark shark2.pcapng &                                                                
[1] 48783

┌──(armando㉿kali)-[~/picoCTF/forensic/wiresharktwootwoootwotwoo]
└─$ Warning: program compiled against libxml 212 using older 209
```
- Notamos que la mayoría son repeticiones, por lo que copiamos los que son diferentes.
```bash
1633	9.334169	192.168.38.104	18.217.1.57	DNS	93	Standard query 0xdf26 A cGljb0NU.reddshrimpandherring.com
2042	11.870534	192.168.38.104	18.217.1.57	DNS	93	Standard query 0x3a30 A RntkbnNf.reddshrimpandherring.com
2444	14.503146	192.168.38.104	18.217.1.57	DNS	93	Standard query 0x531d A M3hmMWxf.reddshrimpandherring.com
3140	16.404809	192.168.38.104	18.217.1.57	DNS	93	Standard query 0x99dd A ZnR3X2Rl.reddshrimpandherring.com
3429	18.239530	192.168.38.104	18.217.1.57	DNS	93	Standard query 0x16f6 A YWRiZWVm.reddshrimpandherring.com
3969	20.266171	192.168.38.104	18.217.1.57	DNS	89	Standard query 0xbe68 A fQ==.reddshrimpandherring.com
```
- Extraemos el texto extraño que contiene cada registro en la información y notamos que al juntar los textos forman una cadena codificada en `Base64` por lo que lo escribimos y lo decodificamos.
```bash
cGljb0NU
RntkbnNf
M3hmMWxf
ZnR3X2Rl
YWRiZWVm
fQ==

cGljb0NURntkbnNfM3hmMWxfZnR3X2RlYWRiZWVmfQ==

[1]  + done       wireshark shark2.pcapng

┌──(armando㉿kali)-[~/picoCTF/forensic/wiresharktwootwoootwotwoo]
└─$ echo cGljb0NURntkbnNfM3hmMWxfZnR3X2RlYWRiZWVmfQ== | base64 -d
```

## Notas Adicionales
## Referencias
