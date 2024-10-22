## Objetivo
The Network Operations Center (NOC) of your local institution picked up a suspicious file, they're getting conflicting information on what type of file it is. They've brought you in as an external expert to examine the file. Can you extract all the information from this strange file?Download the suspicious file [here](https://artifacts.picoctf.net/c_titan/97/flag2of2-final.pdf).
## Solución

```bash
┌──(armando㉿kali)-[~/picoCTF/forensic/secretofthepolyglot]
└─$ ls
flag2of2-final.pdf
```
- Este archivo contiene la segunda parte de la bandera.
```bash
┌──(armando㉿kali)-[~/picoCTF/forensic/secretofthepolyglot]
└─$ open flag2of2-final.pdf 

1n_pn9_&_pdf_724b1287}
```
- Verificamos que tipo de archivo es, le cambiamos la extensión por la correcta y abrimos la imagen.
```bash
┌──(armando㉿kali)-[~/picoCTF/forensic/secretofthepolyglot]
└─$ file flag2of2-final.pdf               
flag2of2-final.pdf: PNG image data, 50 x 50, 8-bit/color RGBA, non-interlaced

┌──(armando㉿kali)-[~/picoCTF/forensic/secretofthepolyglot]
└─$ mv flag2of2-final.pdf flag2of2-final.png            

┌──(armando㉿kali)-[~/picoCTF/forensic/secretofthepolyglot]
└─$ eog flag2of2-final.png               

picoCTF{f1u3n7_

┌──(armando㉿kali)-[~/picoCTF/forensic/secretofthepolyglot]
└─$
```

## Notas Adicionales
## Referencias