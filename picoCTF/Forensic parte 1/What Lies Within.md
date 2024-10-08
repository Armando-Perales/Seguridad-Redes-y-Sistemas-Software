## Objetivo
There's something in the [building](https://jupiter.challenges.picoctf.org/static/011955b303f293d60c8116e6a4c5c84f/buildings.png). Can you retrieve the flag?
## Solución 1
- Usamos la pagina https://stylesuxx.github.io/steganography/ para deocdificar la imagen y obtener la bandera.
## Solución 2
- Instalamos la herramienta `zsteg` para detectar datos ocultos y la utilizamos con el archivo junto con un grep para encontrar la bandera.
```bash
┌──(armando㉿kali)-[~/picoCTF/forensic/whatlieswithin]
└─$ sudo gem install zsteg 

...

┌──(armando㉿kali)-[~/picoCTF/forensic/whatlieswithin]
└─$ zsteg -a buildings.png | grep pico
b1,rgb,lsb,xy       .. text: "picoCTF{h1d1ng_1n_th3_b1t5}"

┌──(armando㉿kali)-[~/picoCTF/forensic/whatlieswithin]
└─$
```

## Notas Adicionales
## Referencias