## Objetivo
Download this packet capture and find the flag.

- [Download packet capture](https://artifacts.picoctf.net/c/134/capture.flag.pcap)
## Solución
- Abrimos el archivo con el wire shark.
```bash
┌──(armando㉿kali)-[~/picoCTF/forensic/eavesdrop]
└─$ ls
capture.flag.pcap

┌──(armando㉿kali)-[~/picoCTF/forensic/eavesdrop]
└─$ file capture.flag.pcap 
capture.flag.pcap: pcap capture file, microsecond ts (little-endian) - version 2.4 (Ethernet, capture length 262144)

┌──(armando㉿kali)-[~/picoCTF/forensic/eavesdrop]
└─$ wireshark capture.flag.pcap &                                
[1] 6122

┌──(armando㉿kali)-[~/picoCTF/forensic/eavesdrop]
└─$ Warning: program compiled against libxml 212 using older 209
```
- Seleccionamos un archivo > Follow > TCP Steam; aquí nos muestra una conversación en donde le envía el comando para descomprimir el archivo y en que puerto se va a enviar el archivo.
```
Hey, how do you decrypt this file again?

You're serious?

Yeah, I'm serious

*sigh* openssl des3 -d -salt -in file.des3 -out file.txt -k supersecretpassword123

Ok, great, thanks.

Let's use Discord next time, it's more secure.

C'mon, no one knows we use this program like this!

Whatever.

Hey.

Yeah?

Could you transfer the file to me again?

Oh great. Ok, over 9002?

Yeah, listening.

Sent it

Got it.

You're unbelievable
```
- Ahora filtramos la información para que nos de solo aquellos que se enviaron al puerto 9002 colocando el siguiente texto:
```bash
tcp.port == 9002
```
- De los archivos que nos filtro notamos que hay uno que tiene una longitud de 48 mientras que los demás tienen una longitud de 0, a ese archivo le desplegamos sus Datos y le damos clic derecho en `Data > Export Packet Bytes`.
```bash
┌──(armando㉿kali)-[~/picoCTF/forensic/eavesdrop]
└─$ ls
capture.flag.pcap  file.des3
```
- Y ya solo utilizamos el comando que nos dieron anteriormente, esto nos generara un archivo txt el cual contiene la bandera.
```bash
┌──(armando㉿kali)-[~/picoCTF/forensic/eavesdrop]
└─$ openssl des3 -d -salt -in file.des3 -out file.txt -k supersecretpassword123
*** WARNING : deprecated key derivation used.
Using -iter or -pbkdf2 would be better.

┌──(armando㉿kali)-[~/picoCTF/forensic/eavesdrop]
└─$ ls
capture.flag.pcap  file.des3  file.txt

┌──(armando㉿kali)-[~/picoCTF/forensic/eavesdrop]
└─$ cat file.txt 
picoCTF{nc_73115_411_dd54ab67}                                                                                                                
┌──(armando㉿kali)-[~/picoCTF/forensic/eavesdrop]
└─$ 
```
## Notas Adicionales
## Referencias