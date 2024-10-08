## Objetivo
We found this [file](https://jupiter.challenges.picoctf.org/static/ab30fcb7d47364b4190a7d3d40edb551/mystery). Recover the flag.
## Solución
- Identificamos de que tipo es el archivo.
```bash
┌──(armando㉿kali)-[~/picoCTF/forensic/corrup]
└─$ file mystery       
mystery: data

┌──(armando㉿kali)-[~/picoCTF/forensic/corrup]
└─$ xxd -l 30 mystery             
00000000: 8965 4e34 0d0a b0aa 0000 000d 4322 4452  .eN4........C"DR
00000010: 0000 066a 0000 0447 0802 0000 007c       ...j...G.....|

┌──(armando㉿kali)-[~/picoCTF/forensic/corrup]
└─$ xxd -l 200 mystery
00000000: 8965 4e34 0d0a b0aa 0000 000d 4322 4452  .eN4........C"DR
00000010: 0000 066a 0000 0447 0802 0000 007c 8bab  ...j...G.....|..
00000020: 7800 0000 0173 5247 4200 aece 1ce9 0000  x....sRGB.......
00000030: 0004 6741 4d41 0000 b18f 0bfc 6105 0000  ..gAMA......a...
00000040: 0009 7048 5973 aa00 1625 0000 1625 0149  ..pHYs...%...%.I
00000050: 5224 f0aa aaff a5ab 4445 5478 5eec bd3f  R$......DETx^..?
00000060: 8e64 cd71 bd2d 8b20 2080 9041 8302 08d0  .d.q.-.  ..A....
00000070: f9ed 40a0 f36e 407b 9023 8f1e d720 8b3e  ..@..n@{.#... .>
00000080: b7c1 0d70 0374 b503 ae41 6bf8 bea8 fbdc  ...p.t...Ak.....
00000090: 3e7d 2a22 336f de5b 55dd 3d3d f920 9188  >}*"3o.[U.==. ..
000000a0: 3871 2232 eb4f 57cf 14e6 25ff e5ff 5b2c  8q"2.OW...%...[,
000000b0: 168b c562 b158 2c16 8bc5 62b1 582c 161d  ...b.X,...b.X,..
000000c0: d6d7 678b c562 b158                      ..g..b.X
```
- Creamos una copia para que no afecte al original.
```bash
┌──(armando㉿kali)-[~/picoCTF/forensic/corrup]
└─$ cp mystery flag.png                                         

┌──(armando㉿kali)-[~/picoCTF/forensic/corrup]
└─$ open flag.png 

┌──(armando㉿kali)-[~/picoCTF/forensic/corrup]
└─$ exiftool flag.png   
ExifTool Version Number         : 12.76
File Name                       : flag.png
Directory                       : .
File Size                       : 203 kB
File Modification Date/Time     : 2024:10:07 11:08:06-06:00
File Access Date/Time           : 2024:10:07 11:08:19-06:00
File Inode Change Date/Time     : 2024:10:07 11:08:06-06:00
File Permissions                : -rw-rw-r--
File Type                       : PNG
File Type Extension             : png
MIME Type                       : image/png
Warning                         : PNG image did not start with IHDR
SRGB Rendering                  : Perceptual
Gamma                           : 2.2
Pixels Per Unit X               : 2852132389
Pixels Per Unit Y               : 5669
Pixel Units                     : meters
```
- Instalamos la herramienta `pngcheck` para que nos ayude a identificar que errores contiene la imagen.
```bash
┌──(armando㉿kali)-[~/picoCTF/forensic/corrup]
└─$ sudo apt install pngcheck                                 

...

┌──(armando㉿kali)-[~/picoCTF/forensic/corrup]
└─$ pngcheck -v flag.png 
zlib warning:  different version (expected 1.2.13, using 1.3.1)

File: flag.png (202940 bytes)
  invalid chunk name "C"DR" (43 22 44 52)
ERRORS DETECTED in flag.png

┌──(armando㉿kali)-[~/picoCTF/forensic/corrup]
└─$ hexeditor flag.png
```
- Buscamos el hexadecimal 43 22 44 52 y lo cambiamos por 49 49 44 52.
```bash
┌──(armando㉿kali)-[~/picoCTF/forensic/corrup]
└─$ eog flag.png     

┌──(armando㉿kali)-[~/picoCTF/forensic/corrup]
└─$ file flag.png 
flag.png: PNG image data, 1642 x 1095, 8-bit/color RGB, non-interlaced

┌──(armando㉿kali)-[~/picoCTF/forensic/corrup]
└─$ pngcheck -v flag.png
zlib warning:  different version (expected 1.2.13, using 1.3.1)

File: flag.png (202940 bytes)
  chunk IHDR at offset 0x0000c, length 13
    1642 x 1095 image, 24-bit RGB, non-interlaced
  chunk sRGB at offset 0x00025, length 1
    rendering intent = perceptual
  chunk gAMA at offset 0x00032, length 4: 0.45455
  chunk pHYs at offset 0x00042, length 9: 2852132389x5669 pixels/meter
  CRC error in chunk pHYs (computed 38d82c82, expected 495224f0)
ERRORS DETECTED in flag.png

┌──(armando㉿kali)-[~/picoCTF/forensic/corrup]
└─$ hexeditor flag.png 
```
- Cambiamos la resolución cambiando en la línea 00000040 el AA por 00.
```bash
┌──(armando㉿kali)-[~/picoCTF/forensic/corrup]
└─$ eog flag.png       

┌──(armando㉿kali)-[~/picoCTF/forensic/corrup]
└─$ file flag.png       
flag.png: PNG image data, 1642 x 1095, 8-bit/color RGB, non-interlaced

┌──(armando㉿kali)-[~/picoCTF/forensic/corrup]
└─$ pngcheck -v flag.png
zlib warning:  different version (expected 1.2.13, using 1.3.1)

File: flag.png (202940 bytes)
  chunk IHDR at offset 0x0000c, length 13
    1642 x 1095 image, 24-bit RGB, non-interlaced
  chunk sRGB at offset 0x00025, length 1
    rendering intent = perceptual
  chunk gAMA at offset 0x00032, length 4: 0.45455
  chunk pHYs at offset 0x00042, length 9: 5669x5669 pixels/meter (144 dpi)
:  invalid chunk length (too large)
ERRORS DETECTED in flag.png

┌──(armando㉿kali)-[~/picoCTF/forensic/corrup]
└─$ hexeditor flag.png
```
- Cambiamos en la línea 00000050 AA AA por 00 00.
```bash
┌──(armando㉿kali)-[~/picoCTF/forensic/corrup]
└─$ open flag.png 

┌──(armando㉿kali)-[~/picoCTF/forensic/corrup]
└─$ pngcheck -v flag.png
zlib warning:  different version (expected 1.2.13, using 1.3.1)

File: flag.png (202940 bytes)
  chunk IHDR at offset 0x0000c, length 13
    1642 x 1095 image, 24-bit RGB, non-interlaced
  chunk sRGB at offset 0x00025, length 1
    rendering intent = perceptual
  chunk gAMA at offset 0x00032, length 4: 0.45455
  chunk pHYs at offset 0x00042, length 9: 5669x5669 pixels/meter (144 dpi)
  invalid chunk name "�DET" (ffffffab 44 45 54)
ERRORS DETECTED in flag.png

┌──(armando㉿kali)-[~/picoCTF/forensic/corrup]
└─$ open flag.png       

┌──(armando㉿kali)-[~/picoCTF/forensic/corrup]
└─$ hexeditor flag.png
```
- Modificamos la línea 00000050 para que quedara de la siguiente manera:
```bash
00000050  52 24 F0 00  00 FF A5 49   44 41 54 78  5E EC BD 3F

┌──(armando㉿kali)-[~/picoCTF/forensic/corrup]
└─$ open flag.png

┌──(armando㉿kali)-[~/picoCTF/forensic/corrup]
└─$ 
```
- Y al abrir la imagen aparece la bandera.
```bash
picoCTF{c0rrupt10n_1847995}
```
## Notas Adicionales
## Referencias