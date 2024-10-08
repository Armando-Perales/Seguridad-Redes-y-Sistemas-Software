## Objetivo
The password for the next level is stored in the file **data.txt**, which contains base64 encoded data
## Datos de Acceso al Nivel
bandit10
FGUW5ilLVJrxX9kMYMmlN4MgbpfMiqey
## Solución
```bash
bandit10@bandit:~$ ls
data.txt
bandit10@bandit:~$ cat data.txt
VGhlIHBhc3N3b3JkIGlzIGR0UjE3M2ZaS2IwUlJzREZTR3NnMlJXbnBOVmozcVJyCg==
bandit10@bandit:~$ file data.txt
data.txt: ASCII text
bandit10@bandit:~$ base64 -d data.txt
The password is dtR173fZKb0RRsDFSGsg2RWnpNVj3qRr
bandit10@bandit:~$
```
## Notas Adicionales
base64 -d data.txt
	base64 permite codificar y descodificar cadenas de caracteres
## Referencias
-  [Google Search for “comando base64 de linux”](https://www.google.com/search?q=comando+base64+de+linux&sca_esv=eb2743fa5ff9c074&sca_upv=1&ei=ahfOZurjIqnQkPIPxvB-&ved=0ahUKEwjqwLem45WIAxUpKEQIHUa4HwAQ4dUDCA8&uact=5&oq=comando+base64+de+linux&gs_lp=Egxnd3Mtd2l6LXNlcnAiF2NvbWFuZG8gYmFzZTY0IGRlIGxpbnV4MggQIRigARjDBDIIECEYoAEYwwQyCBAhGKABGMMESNAsUJMIWL8ncAN4AZABAJgB8gGgAaUJqgEFMS41LjK4AQPIAQD4AQGYAgqgAoAIwgIKEAAYsAMY1gQYR8ICBhAAGAcYHsICBxAAGIAEGA3CAggQABgHGAgYHsICCBAAGAgYDRgewgIKEAAYBxgIGB4YD8ICCBAAGIAEGKIEwgIIEAAYogQYiQXCAggQABgIGB4YD8ICChAhGKABGMMEGAqYAwCIBgGQBgiSBwUzLjYuMaAH0Sk&sclient=gws-wiz-serp)
- https://gchq.github.io/CyberChef/