## Objetivo
Can you find the robots? `https://jupiter.challenges.picoctf.org/problem/60915/` ([link](https://jupiter.challenges.picoctf.org/problem/60915/)) or http://jupiter.challenges.picoctf.org:60915
## Solución 1
- A la dirección le añadí robots.txt
```
https://jupiter.challenges.picoctf.org/problem/60915/robots.txt
```
- Copie y pegue la pagina que el archivo robots.txt escondía para mi.
```
https://jupiter.challenges.picoctf.org/problem/60915/8028f.html
```

```
picoCTF{ca1cu1at1ng_Mach1n3s_8028f}
```
## Solución 2
```bash
armandopc-picoctf@webshell:~$ curl http://jupiter.challenges.picoctf.org:60915
<!doctype html>
<html>
  <head>
    <title>Welcome</title>
    <link href="https://fonts.googleapis.com/css?family=Monoton|Roboto" rel="stylesheet">
    <link rel="stylesheet" type="text/css" href="style.css">
  </head>

  <body>
    <div class="container">
      <header>
        <h1>Welcome</h1>
      </header>
      <div class="content">
        <p>Where are the robots?</p>
      </div>
      <footer></footer>
    </div>
  </body>
</html>
armandopc-picoctf@webshell:~$ curl http://jupiter.challenges.picoctf.org:60915/robots.txt
User-agent: *
Disallow: /8028f.html
armandopc-picoctf@webshell:~$ curl http://jupiter.challenges.picoctf.org:60915/8028f.html
<!doctype html>
<html>
  <head>
    <title>Where are the robots</title>
    <link href="https://fonts.googleapis.com/css?family=Monoton|Roboto" rel="stylesheet">
    <link rel="stylesheet" type="text/css" href="style.css">
  </head>
  <body>
    <div class="container">
      
      <div class="content">
        <p>Guess you found the robots<br />
          <flag>picoCTF{ca1cu1at1ng_Mach1n3s_8028f}</flag></p>
      </div>
      <footer></footer>
  </body>
</html>
armandopc-picoctf@webshell:~$ 
```
## Notas Adicionales
## Referencias
- [Estándar de exclusión de robots](https://es.wikipedia.org/wiki/Est%C3%A1ndar_de_exclusi%C3%B3n_de_robots)