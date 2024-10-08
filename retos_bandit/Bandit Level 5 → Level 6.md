## Objetivo
The password for the next level is stored in a file somewhere under the **inhere** directory and has all of the following properties:

- human-readable
- 1033 bytes in size
- not executable
## Datos de Acceso al Nivel
bandit5
4oQYVPkxZOOEOO5pTW81FB8j8lxXGUQw
## Solución
```bash
bandit5@bandit:~$ ls
inhere
bandit5@bandit:~$ cd inhere/
bandit5@bandit:~/inhere$ ls
maybehere00  maybehere03  maybehere06  maybehere09  maybehere12  maybehere15  maybehere18
maybehere01  maybehere04  maybehere07  maybehere10  maybehere13  maybehere16  maybehere19
maybehere02  maybehere05  maybehere08  maybehere11  maybehere14  maybehere17
bandit5@bandit:~/inhere$ ls -R
.:
maybehere00  maybehere03  maybehere06  maybehere09  maybehere12  maybehere15  maybehere18
maybehere01  maybehere04  maybehere07  maybehere10  maybehere13  maybehere16  maybehere19
maybehere02  maybehere05  maybehere08  maybehere11  maybehere14  maybehere17

./maybehere00:
-file1  -file2  -file3  spaces file1  spaces file2  spaces file3

./maybehere01:
-file1  -file2  -file3  spaces file1  spaces file2  spaces file3

./maybehere02:
-file1  -file2  -file3  spaces file1  spaces file2  spaces file3

./maybehere03:
-file1  -file2  -file3  spaces file1  spaces file2  spaces file3

./maybehere04:
-file1  -file2  -file3  spaces file1  spaces file2  spaces file3

./maybehere05:
-file1  -file2  -file3  spaces file1  spaces file2  spaces file3

./maybehere06:
-file1  -file2  -file3  spaces file1  spaces file2  spaces file3

./maybehere07:
-file1  -file2  -file3  spaces file1  spaces file2  spaces file3

./maybehere08:
-file1  -file2  -file3  spaces file1  spaces file2  spaces file3

./maybehere09:
-file1  -file2  -file3  spaces file1  spaces file2  spaces file3

./maybehere10:
-file1  -file2  -file3  spaces file1  spaces file2  spaces file3

./maybehere11:
-file1  -file2  -file3  spaces file1  spaces file2  spaces file3

./maybehere12:
-file1  -file2  -file3  spaces file1  spaces file2  spaces file3

./maybehere13:
-file1  -file2  -file3  spaces file1  spaces file2  spaces file3

./maybehere14:
-file1  -file2  -file3  spaces file1  spaces file2  spaces file3

./maybehere15:
-file1  -file2  -file3  spaces file1  spaces file2  spaces file3

./maybehere16:
-file1  -file2  -file3  spaces file1  spaces file2  spaces file3

./maybehere17:
-file1  -file2  -file3  spaces file1  spaces file2  spaces file3

./maybehere18:
-file1  -file2  -file3  spaces file1  spaces file2  spaces file3

./maybehere19:
-file1  -file2  -file3  spaces file1  spaces file2  spaces file3
bandit5@bandit:~/inhere$ find . -type f -size 1033c
./maybehere07/.file2
bandit5@bandit:~/inhere$ cat ./maybehere07/.file2
HWasnPhtq9AVKe0dmk45nxy20cvUa6EG
                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                        
                                        bandit5@bandit:~/inhere$
```
## Notas Adicionales
ls -R - Lista archivos de forma recursiva, es decir, las carpetas con las subcarpetas, etc.
find . -type f -size 1033c
	. significa busca desde aqui hacia abajo
	-type f - especifica que busque un archivo del tipo regular
	-size 1033c - especifica el tamaño del archivo 1033c
	c - byte
## Referencias