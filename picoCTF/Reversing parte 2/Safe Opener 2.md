## Objetivo
What can you do with this file? I forgot the key to my safe but this [file](https://artifacts.picoctf.net/c/291/SafeOpener.class) is supposed to help me with retrieving the lost key. Can you help me unlock my safe?
## Solución 1
- Entramos a las siguiente pagina y le subimos el archivo `class` y lo descompila y nos muestra el código java y la bandera.
- [Java decompiler online](http://javadecompilers.com/)

## Solución 2
- Instalamos la herramienta `jd-gui` el cual es una interfaz grafica que nos ayudara a descompilar el archivo.
```bash
┌──(armando㉿kali)-[~/picoCTF/reversing/safeopener2]
└─$ ls
SafeOpener.class

┌──(armando㉿kali)-[~/picoCTF/reversing/safeopener2]
└─$ file SafeOpener.class 
SafeOpener.class: compiled Java class data, version 52.0 (Java 1.8)

┌──(armando㉿kali)-[~/picoCTF/reversing/safeopener2]
└─$ sudo apt install jd-gui     
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

Installing:
  jd-gui

Summary:
  Upgrading: 0, Installing: 1, Removing: 0, Not Upgrading: 730
  Download size: 1287 kB
  Space needed: 1500 kB / 1003 GB available

Get:1 http://kali.download/kali kali-rolling/main amd64 jd-gui all 1.6.6-0kali1 [1287 kB]
Fetched 1287 kB in 33s (38.7 kB/s)
Selecting previously unselected package jd-gui.
(Reading database ... 417210 files and directories currently installed.)
Preparing to unpack .../jd-gui_1.6.6-0kali1_all.deb ...
Unpacking jd-gui (1.6.6-0kali1) ...
Setting up jd-gui (1.6.6-0kali1) ...
Processing triggers for kali-menu (2024.3.1) ...

┌──(armando㉿kali)-[~/picoCTF/reversing/safeopener2]
└─$ jd-gui 
Picked up _JAVA_OPTIONS: -Dawt.useSystemAAFontSettings=on -Dswing.aatext=true

┌──(armando㉿kali)-[~/picoCTF/reversing/safeopener2]
└─$ 
```
- Abrimos la herramienta y le insertamos el archivo, y ya nos mostrara tanto el código como la bandera.

![[20241030103208.png]]

## Solución 3
- Le aplicamos un `strings` junto con un `grep`.
```bash
┌──(armando㉿kali)-[~/picoCTF/reversing/safeopener2]
└─$ strings SafeOpener.class | grep pico
,picoCTF{SAf3_0p3n3rr_y0u_solv3d_it_198203f7}

┌──(armando㉿kali)-[~/picoCTF/reversing/safeopener2]
└─$ 

```

## Notas Adicionales
## Referencias