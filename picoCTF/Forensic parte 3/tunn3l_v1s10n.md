## Objetivo
We found this [file](https://mercury.picoctf.net/static/da18eed3d15fd04f7b076bdcecf15b27/tunn3l_v1s10n). Recover the flag.
## Solución
```bash
┌──(armando㉿kali)-[~/picoCTF/forensic/tunn3lvis10n]
└─$ ls
tunn3l_v1s10n

┌──(armando㉿kali)-[~/picoCTF/forensic/tunn3lvis10n]
└─$ file tunn3l_v1s10n 
tunn3l_v1s10n: data

┌──(armando㉿kali)-[~/picoCTF/forensic/tunn3lvis10n]
└─$ exiftool tunn3l_v1s10n 
ExifTool Version Number         : 12.76
File Name                       : tunn3l_v1s10n
Directory                       : .
File Size                       : 2.9 MB
File Modification Date/Time     : 2021:03:15 12:24:47-06:00
File Access Date/Time           : 2024:10:09 10:27:44-06:00
File Inode Change Date/Time     : 2024:10:09 10:27:24-06:00
File Permissions                : -rw-rw-r--
File Type                       : BMP
File Type Extension             : bmp
MIME Type                       : image/bmp
BMP Version                     : Unknown (53434)
Image Width                     : 1134
Image Height                    : 306
Planes                          : 1
Bit Depth                       : 24
Compression                     : None
Image Length                    : 2893400
Pixels Per Meter X              : 5669
Pixels Per Meter Y              : 5669
Num Colors                      : Use BitDepth
Num Important Colors            : All
Red Mask                        : 0x27171a23
Green Mask                      : 0x20291b1e
Blue Mask                       : 0x1e212a1d
Alpha Mask                      : 0x311a1d26
Color Space                     : Unknown (,5%()
Rendering Intent                : Unknown (826103054)
Image Size                      : 1134x306
Megapixels                      : 0.347

┌──(armando㉿kali)-[~/picoCTF/forensic/tunn3lvis10n]
└─$ xxd -l 100 tunn3l_v1s10n      
00000000: 424d 8e26 2c00 0000 0000 bad0 0000 bad0  BM.&,...........
00000010: 0000 6e04 0000 3201 0000 0100 1800 0000  ..n...2.........
00000020: 0000 5826 2c00 2516 0000 2516 0000 0000  ..X&,.%...%.....
00000030: 0000 0000 0000 231a 1727 1e1b 2920 1d2a  ......#..'..) .*
00000040: 211e 261d 1a31 2825 352c 2933 2a27 382f  !.&..1(%5,)3*'8/
00000050: 2c2f 2623 332a 262d 2420 3b32 2e32 2925  ,/&#3*&-$ ;2.2)%
00000060: 3027 2333                                0'#3

┌──(armando㉿kali)-[~/picoCTF/forensic/tunn3lvis10n]
└─$ hexeditor tunn3l_v1s10n 
```
- Modificamos el header del archivo para que quede de la siguiente forma:
```bash
00000000  42 4D 8E 26  2C 00 00 00   00 00 28 00  00 00 28 00
```

```bash
┌──(armando㉿kali)-[~/picoCTF/forensic/tunn3lvis10n]
└─$ eog tunn3l_v1s10n     

┌──(armando㉿kali)-[~/picoCTF/forensic/tunn3lvis10n]
└─$ xxd -l 100 tunn3l_v1s10n
00000000: 424d 8e26 2c00 0000 0000 2800 0000 2800  BM.&,.....(...(.
00000010: 0000 6e04 0000 3201 0000 0100 1800 0000  ..n...2.........
00000020: 0000 5826 2c00 2516 0000 2516 0000 0000  ..X&,.%...%.....
00000030: 0000 0000 0000 231a 1727 1e1b 2920 1d2a  ......#..'..) .*
00000040: 211e 261d 1a31 2825 352c 2933 2a27 382f  !.&..1(%5,)3*'8/
00000050: 2c2f 2623 332a 262d 2420 3b32 2e32 2925  ,/&#3*&-$ ;2.2)%
00000060: 3027 2333                                0'#3

┌──(armando㉿kali)-[~/picoCTF/forensic/tunn3lvis10n]
└─$ exiftool tunn3l_v1s10n
ExifTool Version Number         : 12.76
File Name                       : tunn3l_v1s10n
Directory                       : .
File Size                       : 2.9 MB
File Modification Date/Time     : 2024:10:09 10:36:32-06:00
File Access Date/Time           : 2024:10:09 10:36:39-06:00
File Inode Change Date/Time     : 2024:10:09 10:36:32-06:00
File Permissions                : -rw-rw-r--
File Type                       : BMP
File Type Extension             : bmp
MIME Type                       : image/bmp
BMP Version                     : Windows V3
Image Width                     : 1134
Image Height                    : 306
Planes                          : 1
Bit Depth                       : 24
Compression                     : None
Image Length                    : 2893400
Pixels Per Meter X              : 5669
Pixels Per Meter Y              : 5669
Num Colors                      : Use BitDepth
Num Important Colors            : All
Image Size                      : 1134x306
Megapixels                      : 0.347

┌──(armando㉿kali)-[~/picoCTF/forensic/tunn3lvis10n]
└─$ hexeditor tunn3l_v1s10n
```
- Se modifico el height para que quedara así:
```bash
00000010  00 00 6E 04  00 00 3A 05
```
- Y ya solo abrimos la imagen y solo transcribimos la bandera.
```bash
picoCTF{qu1t3_a_v13w_2020}
```
## Notas Adicionales
## Referencias