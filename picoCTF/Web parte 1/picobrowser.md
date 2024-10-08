## Objetivo
This website can be rendered only by **picobrowser**, go and catch the flag! `https://jupiter.challenges.picoctf.org/problem/50522/` ([link](https://jupiter.challenges.picoctf.org/problem/50522/)) or http://jupiter.challenges.picoctf.org:50522
## Solución 1
- Inspecciono la pagina, me voy a red, vuelvo a generar la petición, tomo la segunda petición (la que genero un estado 200), me voy al encabezado de petición, le digo Reenviar, me voy a User-Agent, cambio el valor por picobrowser lo envío y la obtengo en la opción que dice Respuesta.
```
picoCTF{p1c0_s3cr3t_ag3nt_51414fa7}
```
## Solución 2
```
armandopc-picoctf@webshell:~$ curl -s http://jupiter.challenges.picoctf.org:50522 -H 'User-Agent: picobrowser' | grep picoCTF
            <p style="text-align:center; font-size:30px;"><b>Flag</b>: <code>picoCTF{p1c0_s3cr3t_ag3nt_51414fa7}</code></p>
```
## Notas Adicionales
## Referencias