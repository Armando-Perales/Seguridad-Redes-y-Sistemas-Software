## Objetivo
The password for the next level is stored in the file **data.txt**, where all lowercase (a-z) and uppercase (A-Z) letters have been rotated by 13 positions
## Datos de Acceso al Nivel
bandit11
dtR173fZKb0RRsDFSGsg2RWnpNVj3qRr
## Solución
```bash
bandit11@bandit:~$ ls
data.txt
bandit11@bandit:~$ cat data.txt
Gur cnffjbeq vf 7k16JArUVv5LxVuJfsSVdbbtaHGlw9D4
bandit11@bandit:~$ cat data.txt | tr '[A-Za-z]' '[N-ZA-Mn-za-m]'
The password is 7x16WNeHIi5YkIhWsfFIqoognUTyj9Q4
bandit11@bandit:~$
```
## Notas Adicionales
ROT-13 - rota los caracteres 13 posiciones en el alfabeto
cat data.txt | tr '[A-Za-z]' '[N-ZA-Mn-za-m]'
	tr permite el reemplazo o eliminación de un conjunto de caracteres
	'[A-Za-z]' - Conjunto de caracteres que se buscaran en un texto
	'[N-ZA-Mn-za-m]' - Conjunto de caracteres que se usarán para modificar un texto, en este caso para decodificar el ROT-13
## Referencias
- [Rot13 en Wikipedia](https://en.wikipedia.org/wiki/ROT13) 
- [Google Search for “comando tr de linux”](https://www.google.com/search?q=comando+tr+de+linux&sca_esv=eb2743fa5ff9c074&sca_upv=1&source=hp&ei=SxfOZpWPF87SkPIPzue6qQE&iflsig=AL9hbdgAAAAAZs4lW3fwVjXJ0qiC-safcZlf3Dk2oHns&oq=comando+tr+d&gs_lp=Egdnd3Mtd2l6Igxjb21hbmRvIHRyIGQqAggAMgYQABgWGB4yCBAAGBYYHhgPMggQABgWGB4YDzIIEAAYFhgeGA8yCBAAGIAEGKIEMggQABiABBiiBEi3I1AAWMgZcAB4AJABAJgB4AGgAZMMqgEFMi44LjK4AQPIAQD4AQGYAgygAu8MwgILEAAYgAQYsQMYgwHCAhEQLhiABBixAxjRAxiDARjHAcICDhAAGIAEGLEDGIMBGIoFwgIFEAAYgATCAg4QLhiABBixAxjRAxjHAcICBRAuGIAEwgIIEAAYgAQYsQPCAg4QABiABBixAxiDARjJA8ICCxAAGIAEGLEDGIoFwgILEAAYgAQYkgMYigXCAggQLhiABBixA8ICCxAuGIAEGLEDGIMBmAMAkgcGMC4xMC4yoAf8eg&sclient=gws-wiz)
-  [Google Search for “rot13 decoder linux”](https://www.google.com/search?q=rot13+decoder+linux&sca_esv=eb2743fa5ff9c074&sca_upv=1&ei=vxjOZqeOHZWfkPIP2LXpwQw&oq=rot13+decoder+&gs_lp=Egxnd3Mtd2l6LXNlcnAiDnJvdDEzIGRlY29kZXIgKgIIATIHEAAYgAQYEzIHEAAYgAQYEzIHEAAYgAQYEzIIEAAYExgWGB4yCBAAGBMYFhgeMggQABgTGBYYHjIIEAAYExgWGB4yCBAAGBMYFhgeMggQABgTGBYYHjIIEAAYExgWGB5In-UQUPPEEFiw2xBwAXgBkAEAmAGmA6ABuwiqAQkwLjEuMS4xLjG4AQPIAQD4AQGYAgWgAuUIwgIKEAAYsAMY1gQYR8ICCxAuGIAEGLEDGIMBwgIFEAAYgATCAggQLhiABBixA8ICCxAAGIAEGLEDGIMBwgIOEC4YgAQYsQMYgwEY1ALCAg4QABiABBixAxiDARiKBcICGhAuGIAEGLEDGIMBGJcFGNwEGN4EGOAE2AEBwgIKEAAYgAQYQxiKBcICEBAuGIAEGLEDGEMYgwEYigXCAggQABiABBixA8ICDhAuGIAEGLEDGNEDGMcBmAMAiAYBkAYCugYGCAEQARgUkgcJMS4xLjEuMS4xoAe9Ng&sclient=gws-wiz-serp)