## Objetivo
The password for the next level is stored in a file called **spaces in this filename** located in the home directory
## Datos de Acceso al Nivel
bandit2
263JGJPfgU6LtdEvgfWU1XP5yac29mFx
## Solución
```bash
bandit2@bandit:~$ ls
spaces in this filename
bandit2@bandit:~$ cat spaces\ in\ this\ filename
MNk8KNH3Usiio41PRUEoDFPqfxLPlSmx
bandit2@bandit:~$ cat "spaces in this filename"
MNk8KNH3Usiio41PRUEoDFPqfxLPlSmx
bandit2@bandit:~$ 
```

## Notas Adicionales
Si el nombre del archivo contiene espacios
	- usar \\ antes del espacio para cada espacio
	- delimitar el nombre del archivo con ""
## Referencias
- [Google Search for “spaces in filename”](https://www.google.com/search?q=spaces+in+filename)