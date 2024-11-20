## Objetivo
A musician left us a [message](https://jupiter.challenges.picoctf.org/static/d5570d48262dbba2a31f2a940409ad9d/message.txt). What's it mean?
## Solución

```bash
┌──(armando㉿kali)-[~/picoCTF/crypto/Mr-Worldwide]
└─$ ls
message.txt

┌──(armando㉿kali)-[~/picoCTF/crypto/Mr-Worldwide]
└─$ file message.txt 
message.txt: ASCII text, with no line terminators

┌──(armando㉿kali)-[~/picoCTF/crypto/Mr-Worldwide]
└─$ cat message.txt 
picoCTF{(35.028309, 135.753082)(46.469391, 30.740883)(39.758949, -84.191605)(41.015137, 28.979530)(24.466667, 54.366669)(3.140853, 101.693207)_(9.005401, 38.763611)(-3.989038, -79.203560)(52.377956, 4.897070)(41.085651, -73.858467)(57.790001, -152.407227)(31.205753, 29.924526)}                                                                                                                    
┌──(armando㉿kali)-[~/picoCTF/crypto/Mr-Worldwide]
└─$ 
```
- Notamos que la bandera esta formada por una cierta cantidad de coordenadas, por lo que con ayuda de `Google Maps` buscamos que lugares conforman la bandera.
```bash
Kyoto, Japan				
Odessa, Ukraine				
Dayton, United States			
Istanbul, Turkey			
Abu Dhabi, United Arab Emirates		
Kuala Lumpur, Malaysia			
_					
Addis Ababa, Ethiophia			
Loja, Ecuador				
Amsterdam, Netherlands			
Sleepy Hollow, United States		
Kodiak, United States			
Alexandria, Egypt
```
- Despues tomamos la primera letra de la ciudad de cada lugar obtenido y con eso formamos la bandera.
```bash
picoCTF{KODIAK_ALASKA}
```

## Notas Adicionales
## Referencias