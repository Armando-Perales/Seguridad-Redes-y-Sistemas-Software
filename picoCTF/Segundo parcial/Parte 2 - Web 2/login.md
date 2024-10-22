## Objetivo
My dog-sitter's brother made this website but I can't get in; can you help?[login.mars.picoctf.net](https://login.mars.picoctf.net/)
## Solución
- Entramos al código fuente de la pagina.
- Luego entramos al archivo de JavaScript que ejecuta:
```bash
<script src="index.js"></script>
```
- El archivo JavaScript compara tanto el usuario como la contraseña que se le envía codificándola en base64 para compararlas con las condiciones para acceder.
- Utilizando CyberChef copiamos el valor con el que compara la contraseña y le aplicamos la operación de `From Base64` decodificaremos el texto para la contraseña el cual es la bandera:
```bash
Texto codificado: "cGljb0NURns1M3J2M3JfNTNydjNyXzUzcnYzcl81M3J2M3JfNTNydjNyfQ"
Texto decodificado: picoCTF{53rv3r_53rv3r_53rv3r_53rv3r_53rv3r}
```

## Notas Adicionales
## Referencias