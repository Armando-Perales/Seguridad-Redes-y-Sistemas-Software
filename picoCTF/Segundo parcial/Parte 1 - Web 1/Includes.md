## Objetivo
Can you get the flag?Go to this [website](http://saturn.picoctf.net:51113/) and see what you can discover.
## Solución
- Vemos el código fuente de la pagina.
- Vemos parte de la bandera en la hoja de estilos.
```css
body {
  background-color: lightblue;
}

/*  picoCTF{1nclu51v17y_1of2_  */
```
- Y vemos el resto de la bandera en el archivo JavaScript
```javaScript
function greetings()
{
  alert("This code is in a separate file!");
}

//  f7w_2of2_6edef411}
```
- Y ya solo juntamos ambas partes.
```bash
picoCTF{1nclu51v17y_1of2_f7w_2of2_6edef411}
```

## Notas Adicionales
## Referencias