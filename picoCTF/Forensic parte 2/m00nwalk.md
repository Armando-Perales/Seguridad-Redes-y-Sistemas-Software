## Objetivo
Decode this [message](https://jupiter.challenges.picoctf.org/static/14393e18d98fedbaedbc28896d7ef31a/message.wav) from the moon.
## Solución
```bash
┌──(armando㉿kali)-[~/picoCTF/forensic/moonwalk]
└─$ file message.wav             
message.wav: RIFF (little-endian) data, WAVE audio, Microsoft PCM, 16 bit, mono 48000 Hz

┌──(armando㉿kali)-[~]
└─$ cd /opt    
```
- Clonamos el repositorio el cual contiene la herramienta `sstv` que nos va ayudar.
```bash
┌──(armando㉿kali)-[/opt]
└─$ sudo git clone https://github.com/colaclanth/sstv.git

...

┌──(armando㉿kali)-[/opt]
└─$ cd sstv        
```
- Instalamos la herramienta que nos ayudara a transformar el archivo.
```bash
┌──(armando㉿kali)-[/opt/sstv]
└─$ sudo python setup.py install

...

┌──(armando㉿kali)-[/opt/sstv]
└─$ cd /home/armando/picoCTF/forensic/moonwalk 

┌──(armando㉿kali)-[~/picoCTF/forensic/moonwalk]
└─$ sstv -d message.wav -o flag.jpg
[sstv] Searching for calibration header... Found!    
[sstv] Detected SSTV mode Scottie 1
[sstv] Decoding image...   [##############################################################################] 100%
[sstv] Drawing image data...
[sstv] ...Done!

┌──(armando㉿kali)-[~/picoCTF/forensic/moonwalk]
└─$ ls
flag.jpg  message.wav

┌──(armando㉿kali)-[~/picoCTF/forensic/moonwalk]
└─$  eog flag.jpg     

┌──(armando㉿kali)-[~/picoCTF/forensic/moonwalk]
└─$
```
- En la imagen se encuentra la bandera.
```bash
picoCTF{beep_boop_im_in_space}
```
## Notas Adicionales
## Referencias