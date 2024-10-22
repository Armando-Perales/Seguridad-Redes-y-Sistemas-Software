## Objetivo
I sent out 2 invitations to all of my friends for my birthday! I'll know if they get stolen because the two invites look similar, and they even have the same md5 hash, but they are slightly different! You wouldn't believe how long it took me to find a collision. Anyway, see if you're invited by submitting 2 PDFs to my website. [http://mercury.picoctf.net:50970/](http://mercury.picoctf.net:50970/)
## Solución
- La pagina nos solicita 2 archivos MD5 por lo que con la ayuda esta pagina encontraremos 2 archivos MD5 parecidos pero un poco diferentes:
```bash
https://www.mscs.dal.ca/~selinger/md5collision/

┌──(armando㉿kali)-[~/picoCTF/web/itsmybirthday]
└─$ ls
erase  hello
```
- Le agregamos la extensión PDF para que la pagina nos acepte los archivo.
```bash
┌──(armando㉿kali)-[~/picoCTF/web/itsmybirthday]
└─$ mv erase erase.pdf

┌──(armando㉿kali)-[~/picoCTF/web/itsmybirthday]
└─$ mv hello hello.pdf

┌──(armando㉿kali)-[~/picoCTF/web/itsmybirthday]
└─$ ls
erase.pdf  hello.pdf

┌──(armando㉿kali)-[~/picoCTF/web/itsmybirthday]
└─$ 
```
- Le enviamos los archivos a la pagina y al darle "Upload" nos mostrara el código php de la pagina y ahí se encuentra la bandera.
```bash
// FLAG: picoCTF{c0ngr4ts_u_r_1nv1t3d_73b0c8ad}
```
## Notas Adicionales
## Referencias
- [MD5 - Wikipedia, la enciclopedia libre](https://es.wikipedia.org/wiki/MD5)