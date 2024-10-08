## Objetivo
There is some interesting information hidden around this site [http://mercury.picoctf.net:44070/](http://mercury.picoctf.net:44070/). Can you find it?
## Solución
- Primero abrimos el código fuente y ahí nos muestra la primera parte de la bandera.
```bash
<!-- Here's the first part of the flag: picoCTF{t -->
```
- Despues entramos a la hoja de estilos del código fuente y ahí se encontrara la segunda parte de la bandera.
```bash
/* CSS makes the page look nice, and yes, it also has part of the flag. Here's part 2: h4ts_4_l0 */
```
- Luego entramos al archivo java Script del código fuente, aquí nos mostrara una pista con la cual nos da a entender que tenemos que entrar al archivo robots.txt, una vez dentro nos mostrara la tercera parte de la bandera y una segunda pista.
```bash
/* How can I keep Google from indexing my website? */

http://mercury.picoctf.net:44070/robots.txt

Part 3: t_0f_pl4c
I think this is an apache server... can you Access the next flag?
```
- Con la pista dada nos indica que tenemos que entrar al fichero del servidor Apache y una vez que hayamos entrado nos dará la cuarta parte de la bandera junto con otra pista para la siguiente parte.
```bash
http://mercury.picoctf.net:44070/.htaccess

Part 4: 3s_2_lO0k
I love making websites on my Mac, I can Store a lot of information there.
```
- Con la pista dada nos indica que tenemos que entrar al archivo de almacenamiento del sistema MacOS y una vez que hayamos entrado nos dará la quinta parte y final de la bandera
```bash
http://mercury.picoctf.net:44070/.DS_Store

Congrats! You completed the scavenger hunt. Part 5: _7a46d25d}
```
## Notas Adicionales
## Referencias
- [Tutorial del Servidor Apache HTTP: Ficheros .htaccess](https://httpd.apache.org/docs/2.4/howto/htaccess.html)
- [.DS_Store](https://en.wikipedia.org/wiki/.DS_Store)