## Objetivo
This [garden](https://jupiter.challenges.picoctf.org/static/d0e1ffb10fc0017c6a82c57900f3ffe3/garden.jpg) contains more than it seems.
## Solución
- Utilizamos la función string en la imagen y le aplicamos un grep para encontrar el texto oculto.
```bash
┌──(armando㉿kali)-[~/picoCTF/forensic/gloryofthegarden]
└─$ strings garden.jpg | grep picoCTF
Here is a flag "picoCTF{more_than_m33ts_the_3y3eBdBd2cc}"

┌──(armando㉿kali)-[~/picoCTF/forensic/gloryofthegarden]
└─$ 
```

## Notas Adicionales
## Referencias
