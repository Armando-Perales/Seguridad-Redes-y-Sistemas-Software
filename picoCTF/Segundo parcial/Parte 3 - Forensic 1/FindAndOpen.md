## Objetivo
Someone might have hidden the password in the trace file.Find the key to unlock [this file](https://artifacts.picoctf.net/c/495/flag.zip). [This tracefile](https://artifacts.picoctf.net/c/495/dump.pcap) might be good to analyze.
## Solución

```bash
┌──(armando㉿kali)-[~/picoCTF/forensic/findAndOpen]
└─$ ls            
dump.pcap  flag.zip

┌──(armando㉿kali)-[~/picoCTF/forensic/findAndOpen]
└─$ file dump.pcap
dump.pcap: pcap capture file, microsecond ts (little-endian) - version 2.4 (Ethernet, capture length 262144)

┌──(armando㉿kali)-[~/picoCTF/forensic/findAndOpen]
└─$ file flag.zip 
flag.zip: Zip archive data, at least v1.0 to extract, compression method=store
```
- Abrimos el archivo pcap con wireshark.
```bash
┌──(armando㉿kali)-[~/picoCTF/forensic/findAndOpen]
└─$ wireshark dump.pcap &
[1] 42394

┌──(armando㉿kali)-[~/picoCTF/forensic/findAndOpen]
└─$ Warning: program compiled against libxml 212 using older 209
```
- Una vez dentro observamos que hay varios archivos que tienen un protocolo diferente al de MDNS por lo que los filtramos.
```bash
!mdns
```
- Al explorar los archivos nos damos cuenta que en realidad son solo 5 archivos diferentes pero uno de ellos parece estar codificada en base64 por lo que la decodificamos.
```bash
┌──(armando㉿kali)-[~/picoCTF/forensic/findAndOpen]
└─$ echo -n aaAABBHHPJGTFRLKVGhpcyBpcyB0aGUgc2VjcmV0OiBwaWNvQ1RGe1IzNERJTkdfTE9LZF8= | base64 -di
i��<���This is the secret: picoCTF{R34DING_LOKd_
```
- Y lo que nos da es la contraseña para poder descomprimir el paquete zip por lo que procedemos a descomprimirlo.
```bash
┌──(armando㉿kali)-[~/picoCTF/forensic/findAndOpen]
└─$ unzip -P picoCTF{R34DING_LOKd_ flag.zip 
Archive:  flag.zip
 extracting: flag                    

┌──(armando㉿kali)-[~/picoCTF/forensic/findAndOpen]
└─$ ls
dump.pcap  flag  flag.zip
```
- Y ya como parte final le aplicamos un cat al archivo que extrajimos del zip y así encontramos la bandera.
```bash
┌──(armando㉿kali)-[~/picoCTF/forensic/findAndOpen]
└─$ cat flag                              
picoCTF{R34DING_LOKd_fil56_succ3ss_0f2afb1a}

┌──(armando㉿kali)-[~/picoCTF/forensic/findAndOpen]
└─$
```
## Notas Adicionales
## Referencias