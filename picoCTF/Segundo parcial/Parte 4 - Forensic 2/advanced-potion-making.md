## Objetivo
Ron just found his own copy of advanced potion making, but its been corrupted by some kind of spell. Help him recover it!

---

| Challenge Endpoints             |                                                                                                                                    |
| ------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------- |
| Download advanced-potion-making | [advanced-potion-making](https://artifacts.picoctf.net/picoMini+by+redpwn/Forensics/advanced-potion-making/advanced-potion-making) |
## Solución
```bash
┌──(armando㉿kali)-[~/picoCTF/forensic/advancedpotionmaking]
└─$ ls
advanced-potion-making

┌──(armando㉿kali)-[~/picoCTF/forensic/advancedpotionmaking]
└─$ file advanced-potion-making
advanced-potion-making: data

┌──(armando㉿kali)-[~/picoCTF/forensic/advancedpotionmaking]
└─$ exiftool advanced-potion-making        
ExifTool Version Number         : 12.76
File Name                       : advanced-potion-making
Directory                       : .
File Size                       : 30 kB
File Modification Date/Time     : 2024:10:21 09:08:10-06:00
File Access Date/Time           : 2024:10:21 09:08:10-06:00
File Inode Change Date/Time     : 2024:10:21 09:08:10-06:00
File Permissions                : -rw-rw-r--
Error                           : Unknown file type

┌──(armando㉿kali)-[~/picoCTF/forensic/advancedpotionmaking]
└─$ hexeditor advanced-potion-making

00000000: 8950 4211 0d0a 1a0a 0012 1314 4948 4452  .PB.........IHDR
00000010: 0000 0990 0000 04d8 0802 0000 0004 2de7  ..............-.
00000020: 7800 0000 0173 5247 4200 aece 1ce9 0000  x....sRGB.......
00000030: 0004 6741 4d41 0000 b18f 0bfc 6105 0000  ..gAMA......a...
00000040: 0009 7048 5973 0000 1625 0000 1625 0149  ..pHYs...%...%.I
00000050: 5224 f000 0076 3949 4441 5478 5eec fd61  R$...v9IDATx^..a
00000060: 72e3 4c94 a659 ce16 6afe 76cd fe57 d7dd  r.L..Y..j.v..W..
00000070: 5b18 45e9 4b8a 7a28 d19d 2048 07a9 6376  [.E.K.z(.. H..cv
00000080: ac2d 2b3e bfaf 5f07 1801 82d7 b2f3 fff3  .-+>.._.........
00000090: fffc 7fff 7f00 0000 0000 0000 4b18 5802  ............K.X.
000000a0: 0000 0000 0000 cb18 5802 0000 0000 0000  ........X.......
000000b0: cb18 5802 0000 0000 0000 cb18 5802 0000  ..X.........X...
000000c0: 0000 0000 cb18 5802 0000 0000 0000 cb18  ......X.........
000000d0: 5802 0000 0000 0000 cb18 5802 0000 0000  X.........X.....
000000e0: 0000 cb18 5802 0000 0000 0000 cb18 5802  ....X.........X.
000000f0: 0000 0000 0000 cb18 5802 0000 0000 0000  ........X.......
00000100: cb18 5802 0000 0000 0000 cb18 5802 0000  ..X.........X...
00000110: 0000 0000 cb18 5802 0000 0000 0000 cb18  ......X.........
00000120: 5802 0000 0000 0000 cb18 5802 0000 0000  X.........X.....
00000130: 0000 cb18 5802 0000 0000 0000 cb18 5802  ....X.........X.
00000140: 0000 0000 0000 cb18 5802 0000 0000 0000  ........X.......
00000150: cb18 5802 0000 0000 0000 cb18 5802 0000  ..X.........X...
```
- Corregimos los bytes la imagen.
```bash
00000000: 8950 4e47 0d0a 1a0a 0000 000d 4948 4452  .PNG........IHDR
00000010: 0000 0990 0000 04d8 0802 0000 0004 2de7  ..............-.
00000020: 7800 0000 0173 5247 4200 aece 1ce9 0000  x....sRGB.......
00000030: 0004 6741 4d41 0000 b18f 0bfc 6105 0000  ..gAMA......a...
00000040: 0009 7048 5973 0000 1625 0000 1625 0149  ..pHYs...%...%.I
00000050: 5224 f000 0076 3949 4441 5478 5eec fd61  R$...v9IDATx^..a
00000060: 72e3 4c94 a659 ce16 6afe 76cd fe57 d7dd  r.L..Y..j.v..W..
00000070: 5b18 45e9 4b8a 7a28 d19d 2048 07a9 6376  [.E.K.z(.. H..cv
00000080: ac2d 2b3e bfaf 5f07 1801 82d7 b2f3 fff3  .-+>.._.........
00000090: fffc 7fff 7f00 0000 0000 0000 4b18 5802  ............K.X.
000000a0: 0000 0000 0000 cb18 5802 0000 0000 0000  ........X.......
000000b0: cb18 5802 0000 0000 0000 cb18 5802 0000  ..X.........X...
000000c0: 0000 0000 cb18 5802 0000 0000 0000 cb18  ......X.........
000000d0: 5802 0000 0000 0000 cb18 5802 0000 0000  X.........X.....
000000e0: 0000 cb18 5802 0000 0000 0000 cb18 5802  ....X.........X.
000000f0: 0000 0000 0000 cb18 5802 0000 0000 0000  ........X.......
00000100: cb18 5802 0000 0000 0000 cb18 5802 0000  ..X.........X...
00000110: 0000 0000 cb18 5802 0000 0000 0000 cb18  ......X.........
00000120: 5802 0000 0000 0000 cb18 5802 0000 0000  X.........X.....
00000130: 0000 cb18 5802 0000 0000 0000 cb18 5802  ....X.........X.
00000140: 0000 0000 0000 cb18 5802 0000 0000 0000  ........X.......
00000150: cb18 5802 0000 0000 0000 cb18 5802 0000  ..X.........X...
```
- Instalamos la herramienta `stegsolver` la cual nos ayudara a desifrar la imagen.
```bash
┌──(armando㉿kali)-[~/picoCTF/forensic/advancedpotionmaking]
└─$ wget http://www.caesum.com/handbook/Stegsolve.jar -O stegosolve.jar
--2024-10-21 09:21:04--  http://www.caesum.com/handbook/Stegsolve.jar
Resolving www.caesum.com (www.caesum.com)... 216.234.165.33
Connecting to www.caesum.com (www.caesum.com)|216.234.165.33|:80... connected.
HTTP request sent, awaiting response... 200 OK
Length: 312271 (305K) [application/x-java-archive]
Saving to: ‘stegosolve.jar’

stegosolve.jar              100%[===========================================>] 304.95K  34.6KB/s    in 9.5s    

2024-10-21 09:21:22 (32.1 KB/s) - ‘stegosolve.jar’ saved [312271/312271]


┌──(armando㉿kali)-[~/picoCTF/forensic/advancedpotionmaking]
└─$ chmod +x stegosolve.jar 

┌──(armando㉿kali)-[~/picoCTF/forensic/advancedpotionmaking]
└─$ java -jar stegosolve.jar                        
Picked up _JAVA_OPTIONS: -Dawt.useSystemAAFontSettings=on -Dswing.aatext=true
```
- Se nos abrirá una pequeña ventana, aquí subes el archivo y ya cuando cargué te vas moviendo con las flechas que tiene abajo hasta encontrar la bandera.
```bash
picoCTF{w1z4rdry}
```

## Notas Adicionales
## Referencias
