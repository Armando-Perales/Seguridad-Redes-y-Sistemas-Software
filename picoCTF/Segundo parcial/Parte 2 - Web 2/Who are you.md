## Objetivo
Let me in. Let me iiiiiiinnnnnnnnnnnnnnnnnnnn [http://mercury.picoctf.net:34588/](http://mercury.picoctf.net:34588/)
## Solución
- Usamos Burp Suite con la pagina y la enviamos a la sección de Repater.
- Como la pagina no deja que entren si no es por PicoBrowse modificamos el Request cambiando el User-Agente por PicoBrowser para que nos deje acceder al sitio.
```bash
User-Agent: PicoBrowser
```
- Ahora nos muestra un mensaje de que no confía en los que la visitan desde otro sitio por lo que agregamos un punto `Referer` para que la pagina vea que no hemos entrado desde otro sitio.
```bash
Referer: mercury.picoctf.net:34588
```
- Ahora nos muestra un mensaje de que este sitio solo funciona en 2018 por lo que añadimos un encabezado de fecha para asegurarnos de que la solicitud se realiza en 2018.
```bash
Date: Wed, 21 Oct 2018 07:28:00 GMT
```
- Ahora nos muestra un mensaje de que no confía en los usuarios que pueden ser rastreados por lo que le añadimos el encabezado de solicitud DNT (Do Not Track) el cual indica la preferencia de seguimiento del usuario.
```bash
DNT: 1
```
- Ahora nos dice que la pagina es para personas de Suecia, así que trabajamos con otro encabezado X-Forward-For.
```bash
X-Forwarded-For: 102.177.146.1
```
- Ahora dice que no hablamos sueco, por lo que tenemos que cambiar el encabezado de idioma a sueco.
```bash
Accept-Language: sv-sv,sv;q=0.5
```
- Y ya con esto obtenemos la bandera
```bash
<b>picoCTF{http_h34d3rs_v3ry_c0Ol_much_w0w_79e451a7}</b>
```

## Notas Adicionales
DNT - Permite a los usuarios indicar si prefieren la privacidad en lugar del contenido personalizado.
X-Forwarded-For - Se agrega automáticamente y lo ayuda a identificar la dirección IP de un cliente cuando usa un balanceador de carga HTTP o HTTPS.

## Referencias