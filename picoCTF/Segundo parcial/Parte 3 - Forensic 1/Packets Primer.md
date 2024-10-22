## Objetivo
Download the packet capture file and use packet analysis software to find the flag.

- [Download packet capture](https://artifacts.picoctf.net/c/194/network-dump.flag.pcap)
## Solución

```bash
┌──(armando㉿kali)-[~/picoCTF/forensic/packetsprimer]
└─$ ls
network-dump.flag.pcap

┌──(armando㉿kali)-[~/picoCTF/forensic/packetsprimer]
└─$ file network-dump.flag.pcap 
network-dump.flag.pcap: pcap capture file, microsecond ts (little-endian) - version 2.4 (Ethernet, capture length 262144)

┌──(armando㉿kali)-[~/picoCTF/forensic/packetsprimer]
└─$ wireshark network-dump.flag.pcap &                                
[1] 3810

┌──(armando㉿kali)-[~/picoCTF/forensic/packetsprimer]
└─$ Warning: program compiled against libxml 212 using older 209

[1]  + done       wireshark network-dump.flag.pcap
┌──(armando㉿kali)-[~/picoCTF/forensic/packetsprimer]
└─$
```
- Abrimos el archivo con wireshark, seleccionamos un archivo que información y le damos clic derecho > Follow > TCP Steam; y despues nos mostrara la bandera.
```bash
picoCTF{p4ck37_5h4rk_ceccaa7f}
```

## Notas Adicionales
## Referencias