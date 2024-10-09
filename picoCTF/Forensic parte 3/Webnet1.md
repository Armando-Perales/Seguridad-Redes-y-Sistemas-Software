## Objetivo
We found this [packet capture](https://jupiter.challenges.picoctf.org/static/fbf98e695555a2a48fe42c9a245de376/capture.pcap) and [key](https://jupiter.challenges.picoctf.org/static/fbf98e695555a2a48fe42c9a245de376/picopico.key). Recover the flag.
## Solución 1
- Entramos con el wireshark y seleccionamos uno de HTTP y ahí buscamos la bandera.
## Solución 2
- File>Export Object>HTTP
- Seleccionamos la imagen y la guardamos
```bash
┌──(armando㉿kali)-[~/picoCTF/forensic/webNet0]
└─$ ls
capture.pcap  picopico.key  vulture.jpg

┌──(armando㉿kali)-[~/picoCTF/forensic/webNet1]
└─$ strings vulture.jpg | grep pico                            
picoCTF{honey.roasted.peanuts}

┌──(armando㉿kali)-[~/picoCTF/forensic/webNet1]
└─$
```
## Solución 3
```bash
┌──(armando㉿kali)-[~/picoCTF/forensic/webNet1]
└─$ ssldump -r capture.pcap -k picopico.key -d | grep pico -A 2 -B 2
Short read: -1295 bytes available (expecting 2)
Short read: -1295 bytes available (expecting 2)
Short read: -1295 bytes available (expecting 2)
Short read: -1295 bytes available (expecting 2)
    0a 43 6f 6e 74 65 6e 74 2d 45 6e 63 6f 64 69 6e    .Content-Encodin
    67 3a 20 67 7a 69 70 0d 0a 50 69 63 6f 2d 46 6c    g: gzip..Pico-Fl
    61 67 3a 20 70 69 63 6f 43 54 46 7b 74 68 69 73    ag: picoCTF{this
    2e 69 73 2e 6e 6f 74 2e 79 6f 75 72 2e 66 6c 61    .is.not.your.fla
    67 2e 61 6e 79 6d 6f 72 65 7d 0d 0a 43 6f 6e 74    g.anymore}..Cont
--
    43 6f 6e 74 65 6e 74 2d 45 6e 63 6f 64 69 6e 67    Content-Encoding
    3a 20 67 7a 69 70 0d 0a 50 69 63 6f 2d 46 6c 61    : gzip..Pico-Fla
    67 3a 20 70 69 63 6f 43 54 46 7b 74 68 69 73 2e    g: picoCTF{this.
    69 73 2e 6e 6f 74 2e 79 6f 75 72 2e 66 6c 61 67    is.not.your.flag
    2e 61 6e 79 6d 6f 72 65 7d 0d 0a 43 6f 6e 74 65    .anymore}..Conte
--
    Accept-Ranges: bytes
    Content-Length: 70395
    Pico-Flag: picoCTF{this.is.not.your.flag.anymore}
    Keep-Alive: timeout=5, max=99
    Connection: Keep-Alive
--
    00 00 00 1f 00 00 00 5a 02 13 00 03 00 00 00 01    .......Z........
    00 01 00 00 00 00 00 00 00 00 00 01 00 00 00 01    ................
    00 00 00 01 00 00 00 01 70 69 63 6f 43 54 46 7b    ........picoCTF{
    68 6f 6e 65 79 2e 72 6f 61 73 74 65 64 2e 70 65    honey.roasted.pe
    61 6e 75 74 73 7d 00 00 ff e2 02 1c 49 43 43 5f    anuts}......ICC_

┌──(armando㉿kali)-[~/picoCTF/forensic/webNet1]
└─$ 
```

## Notas Adicionales
## Referencias