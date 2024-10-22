## Objetivo
Try [here](http://titan.picoctf.net:50989/) to find the flag
## Solución
- Entramos al sitio web y contestamos el primer formulario que nos muestra, al registrarnos nos mostrara un segundo formulario, aquí abrimos la herramienta Burp Suit nos dirigimos a la sección de Proxy, nos dirigimos al apartado de Intercepción y lo encendemos; en la pagina damos un valor cualquiera para el segundo formulario, luego adentro de Burp eliminaremos la ultima línea que aparece:
```bash
opt=flag
```
Una vez eliminada la línea le damos clic a Forward para que continúe con el envió del formulario y ya en la pagina aparecerá la bandera.
```bash
Welcome, armando you sucessfully bypassed the OTP request. Your Flag: picoCTF{#0TP_Bypvss_SuCc3$S_b3fa4f1a}
```

## Notas Adicionales
## Referencias