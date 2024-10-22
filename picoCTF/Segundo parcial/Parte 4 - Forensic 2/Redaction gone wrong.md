## Objetivo
Now you DON’T see me.This [report](https://artifacts.picoctf.net/c/84/Financial_Report_for_ABC_Labs.pdf) has some critical data in it, some of which have been redacted correctly, while some were not. Can you find an important key that was not redacted properly?
## Solución
```bash
┌──(armando㉿kali)-[~/picoCTF/forensic/redactiongonewrong]
└─$ ls                                               
Financial_Report_for_ABC_Labs.pdf

┌──(armando㉿kali)-[~/picoCTF/forensic/redactiongonewrong]
└─$ file Financial_Report_for_ABC_Labs.pdf           
Financial_Report_for_ABC_Labs.pdf: PDF document, version 1.7, 1 page(s)

┌──(armando㉿kali)-[~/picoCTF/forensic/redactiongonewrong]
└─$ open Financial_Report_for_ABC_Labs.pdf            

┌──(armando㉿kali)-[~/picoCTF/forensic/redactiongonewrong]
└─$ 
```
- Ya solo copiamos el texto del archivo.
```bash
picoCTF{C4n_Y0u_S33_m3_fully}
```

## Notas Adicionales
## Referencias