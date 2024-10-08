## Objetivo
This is a really weird text file [TXT](https://jupiter.challenges.picoctf.org/static/e7e5d188621ee705ceeb0452525412ef/flag.txt)? Can you find the flag?
## Solución
- Identificamos que el archivo en verdad sea un archivo `txt`.
```bash
┌──(armando㉿kali)-[~/picoCTF/forensic/extensions]
└─$ file flag.txt    
flag.txt: PNG image data, 1697 x 608, 8-bit/color RGB, non-interlaced
```
- Al saber que en verdad es una imagen, renombramos la extensión por png y utilizamos la herramienta eog para observar la imagen.
```
┌──(armando㉿kali)-[~/picoCTF/forensic/extensions]
└─$ mv flag.txt flag.png            

┌──(armando㉿kali)-[~/picoCTF/forensic/extensions]
└─$ ls
flag.png

┌──(armando㉿kali)-[~/picoCTF/forensic/extensions]
└─$ eog flag.png         

┌──(armando㉿kali)-[~/picoCTF/forensic/extensions]
└─$
```
- En la imagen se encuentra la bandera, ya solo es transcribirla o usar una pagina web para convertir la imagen en texto.
## Notas Adicionales
## Referencias