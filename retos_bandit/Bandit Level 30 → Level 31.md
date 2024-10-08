## Objetivo
There is a git repository at `ssh://bandit30-git@localhost/home/bandit30-git/repo` via the port `2220`. The password for the user `bandit30-git` is the same as for the user `bandit30`.

Clone the repository and find the password for the next level.
## Datos de Acceso al Nivel
bandit30
qp30ex3VLz5MDG1n91YowTv4Q8l7CDZL
## Solución
```bash
bandit30@bandit:~$ mktemp -d
/tmp/tmp.b3fCkgPuLm
bandit30@bandit:~$ cd /tmp/tmp.b3fCkgPuLm
bandit30@bandit:/tmp/tmp.b3fCkgPuLm$ git clone ssh://bandit30-git@localhost:2220/home/bandit30-git/repo
Cloning into 'repo'...
The authenticity of host '[localhost]:2220 ([127.0.0.1]:2220)' can't be established.
ED25519 key fingerprint is SHA256:C2ihUBV7ihnV1wUXRb4RrEcLfXC5CXlhmAAM/urerLY.
This key is not known by any other names.
Are you sure you want to continue connecting (yes/no/[fingerprint])? yes
Could not create directory '/home/bandit30/.ssh' (Permission denied).
Failed to add the host to the list of known hosts (/home/bandit30/.ssh/known_hosts).
                         _                     _ _ _
                        | |__   __ _ _ __   __| (_) |_
                        | '_ \ / _` | '_ \ / _` | | __|
                        | |_) | (_| | | | | (_| | | |_
                        |_.__/ \__,_|_| |_|\__,_|_|\__|


                      This is an OverTheWire game server.
            More information on http://www.overthewire.org/wargames

bandit30-git@localhost's password:
remote: Enumerating objects: 4, done.
remote: Counting objects: 100% (4/4), done.
Receiving objects: 100% (4/4), 298 bytes | 298.00 KiB/s, done.
remote: Total 4 (delta 0), reused 0 (delta 0), pack-reused 0
bandit30@bandit:/tmp/tmp.b3fCkgPuLm$ ls -la
total 10816
drwx------    3 bandit30 bandit30     4096 Sep  6 01:01 .
drwxrwx-wt 5597 root     root     11063296 Sep  6 01:02 ..
drwxrwxr-x    3 bandit30 bandit30     4096 Sep  6 01:02 repo
bandit30@bandit:/tmp/tmp.b3fCkgPuLm$ cd repo
bandit30@bandit:/tmp/tmp.b3fCkgPuLm/repo$ ls -la
total 16
drwxrwxr-x 3 bandit30 bandit30 4096 Sep  6 01:02 .
drwx------ 3 bandit30 bandit30 4096 Sep  6 01:01 ..
drwxrwxr-x 8 bandit30 bandit30 4096 Sep  6 01:02 .git
-rw-rw-r-- 1 bandit30 bandit30   30 Sep  6 01:02 README.md
bandit30@bandit:/tmp/tmp.b3fCkgPuLm/repo$ cat README.md
just an epmty file... muahaha
bandit30@bandit:/tmp/tmp.b3fCkgPuLm/repo$ git tag
secret
bandit30@bandit:/tmp/tmp.b3fCkgPuLm/repo$ git show secret
fb5S2xb7bRyFmAvQYQGEqsbhVyJqhnDy
bandit30@bandit:/tmp/tmp.b3fCkgPuLm/repo$

```
## Notas Adicionales
git tag - Lista las etiquetas en orden alfabético.
git show - Permite ver la información de la etiqueta
## Referencias
- [Fundamentos de Git - Etiquetado](https://git-scm.com/book/es/v2/Fundamentos-de-Git-Etiquetado)