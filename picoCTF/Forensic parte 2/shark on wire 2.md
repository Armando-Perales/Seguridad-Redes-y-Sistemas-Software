## Objetivo
We found this [packet capture](https://jupiter.challenges.picoctf.org/static/b506393b6f9d53b94011df000c534759/capture.pcap). Recover the flag that was pilfered from the network.
## Solución
```bash
┌──(armando㉿kali)-[~/picoCTF/forensic/sharkonwire2]
└─$ file capture.pcap                                    
capture.pcap: pcap capture file, microsecond ts (little-endian) - version 2.4 (Ethernet, capture length 262144)

┌──(armando㉿kali)-[~/picoCTF/forensic/sharkonwire2]
└─$ wireshark capture.pcap &                                                                           
[1] 54508

┌──(armando㉿kali)-[~/picoCTF/forensic/sharkonwire2]
└─$ Warning: program compiled against libxml 212 using older 209

┌──(armando㉿kali)-[~/picoCTF/forensic/sharkonwire2]
└─$ 
[1]  + done       wireshark capture.pcap

┌──(armando㉿kali)-[~/picoCTF/forensic/sharkonwire2]
└─$ nano exp.py
```
- Con el siguiente código buscamos todos los paquetes que fueron entregados al puerto 22 y tomamos el carácter que se obtiene al restarle 5000 al puerto del paquete del cual se envió.
```python
from scapy.all import *

packets = rdpcap('capture.pcap')

flag=''

for p in packets:
        if UDP in p and p[UDP].dport == 22:
                if p[UDP].sport > 5000:
                        flag += chr(p[UDP].sport-5000)
print(flag)
```
- Y al ejecutar el programa obtenemos la bandera.
```bash
┌──(armando㉿kali)-[~/picoCTF/forensic/sharkonwire2]
└─$ python exp.py
picoCTF{p1LLf3r3d_data_v1a_st3g0}

┌──(armando㉿kali)-[~/picoCTF/forensic/sharkonwire2]
└─$ 
```

## Notas Adicionales
## Referencias