## Objetivo
We found this [packet capture](https://jupiter.challenges.picoctf.org/static/483e50268fe7e015c49caf51a69063d0/capture.pcap). Recover the flag.
## Solución
- Abrimos el archivo con la herramienta `Wireshark`.
```bash
┌──(armando㉿kali)-[~/picoCTF/forensic/sharkonwire1]
└─$ wireshark capture.pcap &                                                                          
[1] 17059

┌──(armando㉿kali)-[~/picoCTF/forensic/sharkonwire1]
└─$ Warning: program compiled against libxml 212 using older 209

[1]  + done       wireshark capture.pcap
┌──(armando㉿kali)-[~/picoCTF/forensic/sharkonwire1]
└─$ 
```
- Seleccionamos un archivo con el protocolo UDP, damos un clic derecho y seleccionamos Follow > UDP Stream; y una vez adentro buscamos la bandera.

## Notas Adicionales
## Referencias