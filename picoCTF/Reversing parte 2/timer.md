## Objetivo
You will find the flag after analysing this apk Download [here](https://artifacts.picoctf.net/c/449/timer.apk).
## Solución 1

```bash
┌──(armando㉿kali)-[~/picoCTF/reversing/timer]
└─$ ls
timer.apk

┌──(armando㉿kali)-[~/picoCTF/reversing/timer]
└─$ file timer.apk       
timer.apk: Android package (APK), with zipflinger virtual entry, with APK Signing Block

┌──(armando㉿kali)-[~/picoCTF/reversing/timer]
└─$ exiftool timer.apk 
ExifTool Version Number         : 12.76
File Name                       : timer.apk
Directory                       : .
File Size                       : 4.7 MB
File Modification Date/Time     : 2023:03:15 21:16:09-06:00
File Access Date/Time           : 2024:10:30 10:36:27-06:00
File Inode Change Date/Time     : 2024:10:30 10:36:20-06:00
File Permissions                : -rw-rw-r--
File Type                       : ZIP
File Type Extension             : zip
MIME Type                       : application/zip
Zip Required Version            : 0
Zip Bit Flag                    : 0
Zip Compression                 : Deflated
Zip Modify Date                 : 1981:01:01 01:01:02
Zip CRC                         : 0xdfb66760
Zip Compressed Size             : 51
Zip Uncompressed Size           : 56
Zip File Name                   : META-INF/com/android/build/gradle/app-metadata.properties
Warning                         : [minor] Use the Duplicates option to extract tags for all 751 files
```
- Descomprimimos el archivo puesto que un `apk` es solo un archivo comprimido, le aplicamos un `grep` para ver sonde se encuentra la bandera.
```bash
┌──(armando㉿kali)-[~/picoCTF/reversing/timer]
└─$ unzip timer.apk                        
...    

┌──(armando㉿kali)-[~/picoCTF/reversing/timer]
└─$ ls                                  
AndroidManifest.xml  META-INF  classes.dex  classes2.dex  classes3.dex  kotlin  res  resources.arsc  timer.apk

┌──(armando㉿kali)-[~/picoCTF/reversing/timer]
└─$ grep -R picoCTF                     
grep: classes3.dex: binary file matches
```
- Utilizamos el comando `find` para saber donde se encuentra el archivo que tiene la bandera, una vez hallado le aplicamos un `strings` junto con un `grep` para que muestre la bandera.
```bash
┌──(armando㉿kali)-[~/picoCTF/reversing/timer]
└─$ find . -name classes3.dex 
./classes3.dex

┌──(armando㉿kali)-[~/picoCTF/reversing/timer]
└─$ strings classes3.dex | grep pico    
*picoCTF{t1m3r_r3v3rs3d_succ355fully_17496}

┌──(armando㉿kali)-[~/picoCTF/reversing/timer]
└─$ 
```
## Solución 2
- Instalamos la herramienta `jadx` y abrimos el `gui` que viene con la herramienta, aquí le insertamos el `apk` para que nos muestre su contenido.
```bash
┌──(armando㉿kali)-[~/picoCTF/reversing/timer]
└─$ sudo apt install jadx           
...

┌──(armando㉿kali)-[~/picoCTF/reversing/timer]
└─$ jadx-gui
```
- Seleccionamos la lupa para buscar los archivos que tengan la palabra `picoCTF`, lo abrimos y nos mostrara la bandera.

![[20241030104652.png]]
![[20241030104736.png]]

## Notas Adicionales
## Referencias