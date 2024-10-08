## Objetivo
Find the flag being held on this server to get ahead of the competition [http://mercury.picoctf.net:21939/](http://mercury.picoctf.net:21939/)
## Solución 1
- Inspeccionamos la pagina, nos dirigimos a la sección de Red, seleccionamos el envió, modificamos el envió cambiando el método GET o POST (dependiendo de la opción elegida) por HEAD y lo reenviamos y así obtenemos la bandera.
```bash
picoCTF{r3j3ct_th3_du4l1ty_6ef27873}
```
## Solución 2
```bash
┌──(armando㉿kali)-[~]
└─$ curl -X HEAD http://mercury.picoctf.net:21939/index.php?
Warning: Setting custom HTTP method to HEAD with -X/--request may not work 
Warning: the way you want. Consider using -I/--head instead.

┌──(armando㉿kali)-[~]
└─$ curl -I http://mercury.picoctf.net:21939/index.php?
HTTP/1.1 200 OK
flag: picoCTF{r3j3ct_th3_du4l1ty_6ef27873}
Content-type: text/html; charset=UTF-8

┌──(armando㉿kali)-[~]
└─$ 
```
## Solución 3
- Creamos una proxy con FoxyProxy, con la herramienta de burpsuite nos dirigimos al apartado de Proxy, una vez dentro nos dirigimos al history y verificamos si se registran las peticiones, una vez verificado nos vamos a la sección de Intercepciones y lo encendemos, modificamos el Request del envío por HEAD, lo reenviamos (dándole clic a Forward); despues de reenviarlo nos redirigimos al historial, seleccionamos el ultimo registro y así obtenemos la bandera.
```bash
picoCTF{r3j3ct_th3_du4l1ty_6ef27873}
```

## Notas Adicionales
## Referencias