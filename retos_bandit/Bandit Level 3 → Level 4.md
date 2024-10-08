## Objetivo
The password for the next level is stored in a hidden file in the **inhere** directory.
## Datos de Acceso al Nivel
bandit3
MNk8KNH3Usiio41PRUEoDFPqfxLPlSmx
## Solución
```bash
bandit3@bandit:~$ ls
inhere
bandit3@bandit:~$ cd inhere/
bandit3@bandit:~/inhere$ ls
bandit3@bandit:~/inhere$ ls -la
total 12
drwxr-xr-x 2 root    root    4096 Jul 17 15:57 .
drwxr-xr-x 3 root    root    4096 Jul 17 15:57 ..
-rw-r----- 1 bandit4 bandit3   33 Jul 17 15:57 ...Hiding-From-You
bandit3@bandit:~/inhere$ cat ...Hiding-From-You
2WmrDFRmJIq3IPxneAaMGhap0pFhF3NJ
bandit3@bandit:~/inhere$
```
## Notas Adicionales
ls -la - Lista archivos en formato largo y muestra los que están ocultos
## Referencias
