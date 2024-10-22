## Objetivo
How about some hide and seek heh?Download this [file](https://artifacts.picoctf.net/c/375/trace.pcap) and find the flag.
## Solución

```bash
┌──(armando㉿kali)-[~/picoCTF/forensic/pcappoisoning]
└─$ ls
trace.pcap

┌──(armando㉿kali)-[~/picoCTF/forensic/pcappoisoning]
└─$ file trace.pcap            
trace.pcap: pcap capture file, microsecond ts (little-endian) - version 2.4 (Raw IPv4, capture length 65535)

┌──(armando㉿kali)-[~/picoCTF/forensic/pcappoisoning]
└─$ wireshark trace.pcap &                                
[1] 6428

┌──(armando㉿kali)-[~/picoCTF/forensic/pcappoisoning]
└─$ Warning: program compiled against libxml 212 using older 209

[1]  + done       wireshark trace.pcap
```
- Buscamos manualmente la bandera que se encontraba escondida dentro de los bytes del paquete y no fue hasta el paquete 507 que la encontramos; ya solo quedaba o copiarla desde wireshark o aplicarle un string junto con un grep al archivo pcap.
```bash
┌──(armando㉿kali)-[~/picoCTF/forensic/pcappoisoning]
└─$ strings trace.pcap | grep picoCTF{       
picoCTF{P64P_4N4L7S1S_SU55355FUL_5b6a6061}@~

┌──(armando㉿kali)-[~/picoCTF/forensic/pcappoisoning]
└─$
```
## Notas Adicionales
## Referencias