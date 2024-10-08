## Objetivo
The password for the next level is stored in the only human-readable file in the **inhere** directory. Tip: if your terminal is messed up, try the “reset” command.
## Datos de Acceso al Nivel
bandit4
2WmrDFRmJIq3IPxneAaMGhap0pFhF3NJ
## Solución
```bash
bandit4@bandit:~$ ls
inhere
bandit4@bandit:~$ cd inhere/
bandit4@bandit:~/inhere$ file ./*
./-file00: data
./-file01: data
./-file02: data
./-file03: data
./-file04: data
./-file05: data
./-file06: data
./-file07: ASCII text
./-file08: data
./-file09: data
bandit4@bandit:~/inhere$ cat ./-file07
4oQYVPkxZOOEOO5pTW81FB8j8lxXGUQw
bandit4@bandit:~/inhere$
```
## Notas Adicionales
cat * -  Muestra todos los archivos en el directorio actual, el * es un comodín que significa todo
file - me dice de que tipo es el archivo
## Referencias