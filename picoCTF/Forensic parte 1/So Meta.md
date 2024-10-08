## Objetivo
Find the flag in this [picture](https://jupiter.challenges.picoctf.org/static/89b371a46702a31aa9931a2a2b12f8bf/pico_img.png).
## Solución 1
- Identificamos si en verdad es un archivo PNG o no.
```bash
┌──(armando㉿kali)-[~/picoCTF/forensic/someta]
└─$ file pico_img.png                                                       
pico_img.png: PNG image data, 600 x 600, 8-bit/color RGB, non-interlaced
```
- Instalamos la herramienta `exiftool` para leer el archivo png.
```bash
┌──(armando㉿kali)-[~/picoCTF/forensic/someta]
└─$ sudo apt install exiftool        

...

┌──(armando㉿kali)-[~/picoCTF/forensic/someta]
└─$ exiftool pico_img.png 
ExifTool Version Number         : 12.76
File Name                       : pico_img.png
Directory                       : .
File Size                       : 109 kB
File Modification Date/Time     : 2020:10:26 12:38:23-06:00
File Access Date/Time           : 2024:10:02 10:35:42-06:00
File Inode Change Date/Time     : 2024:10:02 10:35:26-06:00
File Permissions                : -rw-rw-r--
File Type                       : PNG
File Type Extension             : png
MIME Type                       : image/png
Image Width                     : 600
Image Height                    : 600
Bit Depth                       : 8
Color Type                      : RGB
Compression                     : Deflate/Inflate
Filter                          : Adaptive
Interlace                       : Noninterlaced
Software                        : Adobe ImageReady
XMP Toolkit                     : Adobe XMP Core 5.3-c011 66.145661, 2012/02/06-14:56:27
Creator Tool                    : Adobe Photoshop CS6 (Windows)
Instance ID                     : xmp.iid:A5566E73B2B811E8BC7F9A4303DF1F9B
Document ID                     : xmp.did:A5566E74B2B811E8BC7F9A4303DF1F9B
Derived From Instance ID        : xmp.iid:A5566E71B2B811E8BC7F9A4303DF1F9B
Derived From Document ID        : xmp.did:A5566E72B2B811E8BC7F9A4303DF1F9B
Warning                         : [minor] Text/EXIF chunk(s) found after PNG IDAT (may be ignored by some readers)
Artist                          : picoCTF{s0_m3ta_eb36bf44}
Image Size                      : 600x600
Megapixels                      : 0.360

┌──(armando㉿kali)-[~/picoCTF/forensic/someta]
└─$
```

## Solución 2
- Utilizamos la función string en la imagen y le aplicamos un grep para encontrar el texto oculto.
```bash
┌──(armando㉿kali)-[~/picoCTF/forensic/someta]
└─$ strings pico_img.png | grep pico
picoCTF{s0_m3ta_eb36bf44}

┌──(armando㉿kali)-[~/picoCTF/forensic/someta]
└─$ 

```

## Notas Adicionales
## Referencias