## Objetivo
The password for the next level is stored in a file called **-** located in the home directory
## Datos de Acceso al Nivel
bandit1
ZjLjTmM6FvvyRnrb2rfNWOZOTa6ip5If
## Solución
```bash
bandit1@bandit:~$ ls
-
bandit1@bandit:~$ cat -
^C
bandit1@bandit:~$ cat ./-
263JGJPfgU6LtdEvgfWU1XP5yac29mFx
bandit1@bandit:~$ pwd
/home/bandit1
bandit1@bandit:~$ cat /home/bandit1/-
263JGJPfgU6LtdEvgfWU1XP5yac29mFx
bandit1@bandit:~$
```
## Notas Adicionales
Si le paso un - al cat pensara que le quiero pasar un parámetro y se confunde. Entonces, si desea abrir este tipo de archivo, debe especificar la ubicación completa del archivo, como ./-. Por ejemplo, si desea ver qué hay en ese archivo, use cat ./-
pwd - indica el directorio actual
ls - lista el contenido del directorio
cat - concatena archivos e imprime en la salida estándar 
## Referencias
- [Google Search for “dashed filename”](https://www.google.com/search?q=dashed+filename)