## Objetivo
The password for the next level is stored in a file **readme** in the homedirectory. Unfortunately, someone has modified **.bashrc** to log you out when you log in with SSH.
## Datos de Acceso al Nivel
bandit18
x2gLTTjFwMOhQ8oWNbMN362QKxfRqGlO
## Solución
```bash
C:\Users\peral>ssh bandit18@bandit.labs.overthewire.org -p2220 /bin/bash
                         _                     _ _ _
                        | |__   __ _ _ __   __| (_) |_
                        | '_ \ / _` | '_ \ / _` | | __|
                        | |_) | (_| | | | | (_| | | |_
                        |_.__/ \__,_|_| |_|\__,_|_|\__|


                      This is an OverTheWire game server.
            More information on http://www.overthewire.org/wargames

bandit18@bandit.labs.overthewire.org's password:
ls
readme
cat readme
cGWpMaKXVwDUNgPAVJbWYuGHVn9zl3j8
exit

C:\Users\peral>
```
## Notas Adicionales
ssh bandit18@bandit.labs.overthewire.org -p2220 /bin/bash
	- ssh permite que al conectarte puedas ejecutar una serie de comandos (ej. /bin/bash)
```bash
C:\Users\peral>ssh bandit18@bandit.labs.overthewire.org -p2220 /bin/bash
                         _                     _ _ _
                        | |__   __ _ _ __   __| (_) |_
                        | '_ \ / _` | '_ \ / _` | | __|
                        | |_) | (_| | | | | (_| | | |_
                        |_.__/ \__,_|_| |_|\__,_|_|\__|


                      This is an OverTheWire game server.
            More information on http://www.overthewire.org/wargames

bandit18@bandit.labs.overthewire.org's password:
cat .bashrc
```
cat .bashrc - permite ver el comando de inicio
## Referencias
