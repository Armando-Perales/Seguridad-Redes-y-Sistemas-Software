## Objetivo
The password for the next level is stored in the file **data.txt** in one of the few human-readable strings, preceded by several ‘=’ characters.
## Datos de Acceso al Nivel
bandit9
4CKMh1JI91bUIZZPXDqGanal4xvAg0JM
## Solución
```bash
bandit9@bandit:~$ ls
data.txt
bandit9@bandit:~$ file data.txt
data.txt: data
bandit9@bandit:~$ strings data.txt | grep ==
\a!;========== the
========== passwordf
========== isc
========== FGUW5ilLVJrxX9kMYMmlN4MgbpfMiqey
bandit9@bandit:~$
```
## Notas Adicionales
strings data.txt | grep ==
	strimgs muestra las cadenas de caracteres imprimibles que contengan los ficheros

## Referencias