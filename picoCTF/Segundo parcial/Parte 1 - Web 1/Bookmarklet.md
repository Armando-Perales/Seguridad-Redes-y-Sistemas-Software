## Objetivo
Why search for the flag when I can make a bookmarklet to print it for me?Browse [here](http://titan.picoctf.net:61190/), and find the flag!
## Solución
- Inspeccionamos la pagina y nos dirigimos a la parte de consola y colocamos el código que viene.
```javaScript
javascript:(function() {
	var encryptedFlag = "àÒÆÞ¦È¬ëÙ£ÖÓÚåÛÑ¢ÕÓÉÕËÆÒÇÚËí";
	var key = "picoctf";
	var decryptedFlag = "";
	for (var i = 0; i < encryptedFlag.length; i++) {
		decryptedFlag += String.fromCharCode((encryptedFlag.charCodeAt(i) - key.charCodeAt(i % key.length) + 256) % 256);
	}
	alert(decryptedFlag);
})();
```
- Y al ejecutar el código nos muestra la bandera
```bash
picoCTF{p@g3_turn3r_cebccdfe}
```

## Notas Adicionales
## Referencias