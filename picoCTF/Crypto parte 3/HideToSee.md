## Objetivo
How about some hide and seek heh?Look at this image [here](https://artifacts.picoctf.net/c/237/atbash.jpg).
## Solución

```bash
┌──(armando㉿kali)-[~/picoCTF/crypto/basicmod1/hideToSee]
└─$ ls
atbash.jpg

┌──(armando㉿kali)-[~/picoCTF/crypto/basicmod1/hideToSee]
└─$ file atbash.jpg 
atbash.jpg: JPEG image data, JFIF standard 1.01, aspect ratio, density 1x1, segment length 16, baseline, precision 8, 465x455, components 3

┌──(armando㉿kali)-[~/picoCTF/crypto/basicmod1/hideToSee]
└─$ strings atbash.jpg | grep pico

┌──(armando㉿kali)-[~/picoCTF/crypto/basicmod1/hideToSee]
└─$ exiftool atbash.jpg 
ExifTool Version Number         : 12.76
File Name                       : atbash.jpg
Directory                       : .
File Size                       : 52 kB
File Modification Date/Time     : 2023:03:15 21:16:32-06:00
File Access Date/Time           : 2024:10:23 11:38:01-06:00
File Inode Change Date/Time     : 2024:10:23 11:37:22-06:00
File Permissions                : -rw-rw-r--
File Type                       : JPEG
File Type Extension             : jpg
MIME Type                       : image/jpeg
JFIF Version                    : 1.01
Resolution Unit                 : None
X Resolution                    : 1
Y Resolution                    : 1
Image Width                     : 465
Image Height                    : 455
Encoding Process                : Baseline DCT, Huffman coding
Bits Per Sample                 : 8
Color Components                : 3
Y Cb Cr Sub Sampling            : YCbCr4:2:0 (2 2)
Image Size                      : 465x455
Megapixels                      : 0.212

┌──(armando㉿kali)-[~/picoCTF/crypto/basicmod1/hideToSee]
└─$ eog atbash.jpg     

┌──(armando㉿kali)-[~/picoCTF/crypto/basicmod1/hideToSee]
└─$
```
- Instalamos la herramienta de `Steghide` para extraer el texto que se encuentra en la imagen.
```
┌──(armando㉿kali)-[~/picoCTF/crypto/basicmod1/hideToSee]
└─$ sudo apt install steghide        

...

┌──(armando㉿kali)-[~/picoCTF/crypto/basicmod1/hideToSee]
└─$ steghide --extract -sf atbash.jpg
Enter passphrase: 
wrote extracted data to "encrypted.txt".

┌──(armando㉿kali)-[~/picoCTF/crypto/basicmod1/hideToSee]
└─$ cat encrypted.txt 
krxlXGU{zgyzhs_xizxp_05y2z65z}

┌──(armando㉿kali)-[~/picoCTF/crypto/basicmod1/hideToSee]
└─$ 
```
- Y ya con la ayuda de `CyberChef` le aplicamos al texto un `Atbash Cipher` para que nos de la bandera.
```bash
picoCTF{atbash_crack_05b2a65a}
```

## Notas Adicionales
## Referencias