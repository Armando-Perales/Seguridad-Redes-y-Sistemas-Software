## Objetivo
I have these 2 images, can you make a flag out of them? [scrambled1.png](https://mercury.picoctf.net/static/1594c3f1980e3fb93df09a6d02f53904/scrambled1.png) [scrambled2.png](https://mercury.picoctf.net/static/1594c3f1980e3fb93df09a6d02f53904/scrambled2.png)
## Solución 1

```bash
┌──(armando㉿kali)-[~/picoCTF/crypto/pixelated]
└─$ ls
scrambled1.png  scrambled2.png

┌──(armando㉿kali)-[~/picoCTF/crypto/pixelated]
└─$ file scrambled1.png 
scrambled1.png: PNG image data, 256 x 256, 8-bit/color RGB, non-interlaced

┌──(armando㉿kali)-[~/picoCTF/crypto/pixelated]
└─$ file scrambled2.png 
scrambled2.png: PNG image data, 256 x 256, 8-bit/color RGB, non-interlaced

┌──(armando㉿kali)-[~/picoCTF/crypto/pixelated]
└─$ eog scrambled1.png 
```
- Descargamos la herramienta de `Stegsolve`
```bash
┌──(armando㉿kali)-[~/picoCTF/crypto/pixelated]
└─$ cd /                                      

┌──(armando㉿kali)-[/]
└─$ cd opt         

┌──(armando㉿kali)-[/opt]
└─$ sudo wget http://www.caesum.com/handbook/Stegsolve.jar -O stegsolve.jar
[sudo] password for armando: 
--2024-10-23 10:56:04--  http://www.caesum.com/handbook/Stegsolve.jar
Resolving www.caesum.com (www.caesum.com)... 216.234.165.33
Connecting to www.caesum.com (www.caesum.com)|216.234.165.33|:80... connected.
HTTP request sent, awaiting response... 200 OK
Length: 312271 (305K) [application/x-java-archive]
Saving to: ‘stegsolve.jar’

stegsolve.jar                100%[===========================================>] 304.95K  48.7KB/s    in 6.2s    

2024-10-23 10:56:19 (49.0 KB/s) - ‘stegsolve.jar’ saved [312271/312271]


┌──(armando㉿kali)-[/opt]
└─$ ls
microsoft  sstv  stegsolve.jar

┌──(armando㉿kali)-[/opt]
└─$ sudo chmod +x stegsolve.jar                                            

┌──(armando㉿kali)-[/opt]
└─$
```
- Ejecutamos el programa, se nos abrirá una pequeña ventana en la cual insertaremos la primera imagen y le daremos en `Analyze > Image Combiner` y despues se nos abrirá una segunda ventana en la cual solo nos movernos por las flechas hasta encontrar la bandera.
```bash
┌──(armando㉿kali)-[~/picoCTF/crypto/pixelated]
└─$ java -jar /opt/stegsolve.jar 
Picked up _JAVA_OPTIONS: -Dawt.useSystemAAFontSettings=on -Dswing.aatext=true
```

## Solución 2
- Instalamos la herramienta de `Imagemagick`.
```bash
┌──(armando㉿kali)-[~/picoCTF/crypto/pixelated]
└─$ sudo apt install imagemagick     
[sudo] password for armando: 
imagemagick is already the newest version (8:6.9.13.12+dfsg1-1).
imagemagick set to manually installed.
The following packages were automatically installed and are no longer required:
  fonts-liberation2         liblua5.2-0              libqt6sql6t64            python3-diskcache
  ibverbs-providers         libmimalloc2.0           libqt6test6t64           python3-jose
  libarmadillo12            libndctl6                libqt6widgets6t64        python3-lib2to3
  libassuan0                libnghttp3-3             libqt6xml6t64            python3-mistune0
  libavformat60             libplacebo338            librados2                python3-pendulum
  libboost-iostreams1.83.0  libplist3                librav1e0                python3-pytzdata
  libboost-thread1.83.0     libpmem1                 librdmacm1t64            python3-rsa
  libcephfs2                libpoppler134            libre2-10                python3-time-machine
  libdaxctl1                libpostproc57            libroc0.3                python3.11
  libgdal34t64              libpython3.11-dev        libssh-gcrypt-4          python3.11-dev
  libgeos3.12.1t64          libpython3.11-minimal    libsvtav1enc1d1          python3.11-minimal
  libgfapi0                 libpython3.11-stdlib     libu2f-udev              rwho
  libgfrpc0                 libpython3.11t64         libusbmuxd6              rwhod
  libgfxdr0                 libqt6dbus6t64           libwireshark17t64        samba-ad-provision
  libglusterfs0             libqt6gui6t64            libwiretap14t64          samba-dsdb-modules
  libibverbs1               libqt6network6t64        libwsutil15t64           samba-vfs-modules
  libimobiledevice6         libqt6opengl6t64         libx265-199
  libjsoncpp25              libqt6openglwidgets6t64  openjdk-17-jre
  libjxl0.7                 libqt6printsupport6t64   openjdk-17-jre-headless
Use 'sudo apt autoremove' to remove them.

Summary:
  Upgrading: 0, Installing: 0, Removing: 0, Not Upgrading: 480
```
- Convertimos ambas imágenes en una nueva imagen y ya solo la abrimos.
```bash
┌──(armando㉿kali)-[~/picoCTF/crypto/pixelated]
└─$ convert scrambled1.png scrambled2.png -compose Add -composite bandera.png 

┌──(armando㉿kali)-[~/picoCTF/crypto/pixelated]
└─$ ls
bandera.png  flag.bmp  scrambled1.png  scrambled2.png

┌──(armando㉿kali)-[~/picoCTF/crypto/pixelated]
└─$ eog bandera.png    

┌──(armando㉿kali)-[~/picoCTF/crypto/pixelated]
└─$
```

## Solución 3
- Creamos un código en `Python` en el cual combine las dos imágenes en una sola.
```bash
┌──(armando㉿kali)-[~/picoCTF/crypto/pixelated]
└─$ nano exp.py
```

```python
from PIL import Image
import numpy as np

imagen1 = np.asarray(Image.open('scrambled1.png'))
imagen2 = np.asarray(Image.open('scrambled2.png'))

todo = imagen1 + imagen2

print(todo)

nuevaImagen = Image.fromarray(todo)

nuevaImagen.save('lachida.png','PNG')
```
- Ejecutamos el código que creamos.
```bash
┌──(armando㉿kali)-[~/picoCTF/crypto/pixelated]
└─$ python exp.py  
[[[255 255 255]
  [255 255 255]
  [255 255 255]
  ...
  [255 255 255]
  [255 255 255]
  [255 255 255]]

 [[255 255 255]
  [255 255 255]
  [255 255 255]
  ...
  [255 255 255]
  [255 255 255]
  [255 255 255]]

 [[255 255 255]
  [255 255 255]
  [255 255 255]
  ...
  [255 255 255]
  [255 255 255]
  [255 255 255]]

 ...

 [[255 255 255]
  [255 255 255]
  [255 255 255]
  ...
  [255 255 255]
  [255 255 255]
  [255 255 255]]

 [[255 255 255]
  [255 255 255]
  [255 255 255]
  ...
  [255 255 255]
  [255 255 255]
  [255 255 255]]

 [[255 255 255]
  [255 255 255]
  [255 255 255]
  ...
  [255 255 255]
  [255 255 255]
  [255 255 255]]]

┌──(armando㉿kali)-[~/picoCTF/crypto/pixelated]
└─$ ls             
bandera.png  exp.py  flag.bmp  lachida.png  scrambled1.png  scrambled2.png

┌──(armando㉿kali)-[~/picoCTF/crypto/pixelated]
└─$ eog lachida.png 

┌──(armando㉿kali)-[~/picoCTF/crypto/pixelated]
└─$ 
```

## Notas Adicionales
## Referencias