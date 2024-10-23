## Objetivo
In RSA, a small `e` value can be problematic, but what about `N`? Can you decrypt this? [values](https://mercury.picoctf.net/static/3cfeb09681369c26e3f19d886bc1e5d9/values)
## Solución

```bash
┌──(armando㉿kali)-[~/picoCTF/crypto/mindyouPsandQs]
└─$ ls
values

┌──(armando㉿kali)-[~/picoCTF/crypto/mindyouPsandQs]
└─$ cat values       
Decrypt my super sick RSA:
c: 8533139361076999596208540806559574687666062896040360148742851107661304651861689
n: 769457290801263793712740792519696786147248001937382943813345728685422050738403253
e: 65537                                                                                                                
┌──(armando㉿kali)-[~/picoCTF/crypto/mindyouPsandQs]
└─$ 
```
- Con ayuda de la siguiente pagina obtenemos la factorización del valor de n que nos dieron:
- [FactorDB](https://factordb.com/)
- Y ya con los valores de `p` y `q` realizamos las operaciones necesarias para obtener el texto desencriptado y así obtener la bandera.
```bash
┌──(armando㉿kali)-[~/picoCTF/crypto/mindyouPsandQs]
└─$ python3
```
```python
Python 3.12.6 (main, Sep  7 2024, 14:20:15) [GCC 14.2.0] on linux
Type "help", "copyright", "credits" or "license" for more information.
>>> c = 8533139361076999596208540806559574687666062896040360148742851107661304651861689
>>> e = 65537
>>> p = 1617549722683965197900599011412144490161
>>> q = 475693130177488446807040098678772442581573
>>> n = p * q
>>> n
769457290801263793712740792519696786147248001937382943813345728685422050738403253
>>> tn = (p-1) * (q-1)
>>> tn
769457290801263793712740792519696786146770691257482771401340787987731866151331520
>>> d = pow(e,-1,tn)
>>> d
582402748221564772374696843202153883711652351188297188998024166320268538694734273
>>> m = pow(c,d,n)
>>> m
13016382529449106065927291425342535437996222135352905256639629442503647501498237
>>> bytes.fromhex(hex(m)[2:]).decode()
'picoCTF{sma11_N_n0_g0od_45369387}'
>>> 
```
```bash
┌──(armando㉿kali)-[~/picoCTF/crypto/mindyouPsandQs]
└─$
```

## Notas Adicionales
## Referencias