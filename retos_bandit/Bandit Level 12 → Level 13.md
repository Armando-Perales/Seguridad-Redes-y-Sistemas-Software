## Objetivo
The password for the next level is stored in the file **data.txt**, which is a hexdump of a file that has been repeatedly compressed. For this level it may be useful to create a directory under /tmp in which you can work. Use mkdir with a hard to guess directory name. Or better, use the command “mktemp -d”. Then copy the datafile using cp, and rename it using mv (read the manpages!)
## Datos de Acceso al Nivel
bandit12
7x16WNeHIi5YkIhWsfFIqoognUTyj9Q4
## Solución
```bash
bandit12@bandit:~$ xxd -r data.txt | zcat | bzcat | zcat | tar xO | tar xO | bzcat | tar xO | zcat
The password is FO5dwFsc0cbaIiH0h8J2eUks2vdTDwAn
bandit12@bandit:~$
```
## Notas Adicionales
```
Algunos tipos de compresion en Linux
-----------------------------------------------------
ext comp desc ver en consola
-----------------------------------------------------
.gz gzip gzip -d (gunzip) zcat
.bz2 bzip2 bzip2 -d (bunzip2) bzcat
.tar tar tar xf tar xO
----------------------------------------------------

otros (instalar) :
.zip zip unzip (7z x)
.rar rar unrar (7z x)
```
xxd -r data.txt | zcat | bzcat | zcat | tar xO | tar xO | bzcat | tar xO | zcat
	xxd -r - descomprime el archivo del hexdump
	zcat - descomprime el archivos gzip en consola
	bzcat - descomprime el archivos bzip2 en consola
	tar xO - descomprime el archivos tar en consola

## Referencias
- [Hex dump on Wikipedia](https://en.wikipedia.org/wiki/Hex_dump)