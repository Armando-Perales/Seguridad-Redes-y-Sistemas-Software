## Objetivo
he password for the next level is stored **somewhere on the server** and has all of the following properties:

- owned by user bandit7
- owned by group bandit6
- 33 bytes in size
## Datos de Acceso al Nivel
bandit6
HWasnPhtq9AVKe0dmk45nxy20cvUa6EG
## Solución
```bash
bandit6@bandit:~$ find / -user bandit7 -group bandit6 -size 33c 2>/dev/null
/var/lib/dpkg/info/bandit7.password
bandit6@bandit:~$ cat /var/lib/dpkg/info/bandit7.password
morbNTDkSW6jIlUc0ymOdMaLnOlFVAaj
bandit6@bandit:~$
```
## Notas Adicionales
find / -user bandit7 -group bandit6 -size 33c 2>/dev/null
	/ - indica a find que busque desde el directorio raíz
	-user - especifica a que usuario pertenece el archivo
	-group - indica a que grupo pertenece el archivo
	-size - indica el tamaño del archivo
	2>/dev/null - manda la salida de error al dispositivo null, es decir, se oculta al usuario
## Referencias