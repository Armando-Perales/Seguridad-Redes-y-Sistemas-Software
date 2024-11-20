## Objetivo
[crackme.py](https://mercury.picoctf.net/static/be2ba466c6154e42c756bf737ddcecc3/crackme.py)
## Solución

```bash
┌──(armando㉿kali)-[~/picoCTF/reversing/crackme-py]
└─$ ls
crackme.py

┌──(armando㉿kali)-[~/picoCTF/reversing/crackme-py]
└─$ file crackme.py              
crackme.py: Python script, ASCII text executable

┌──(armando㉿kali)-[~/picoCTF/reversing/crackme-py]
└─$ nano crackme.py            
```
- Nos dan el siguiente código que al ejecutarlo simplemente nos devuelve el numero mayor de entre 2 numero que le damos, pero podemos revisar que hay una sección a parte que realiza otras cosas. Lo que hace `decode_secret` es que simplemente hace un ROT47 a lo que se le da como parámetro.
```python
# Hiding this really important number in an obscure piece of code is brilliant!
# AND it's encrypted!
# We want our biggest client to know his information is safe with us.
bezos_cc_secret = "A:4@r%uL`M-^M0c0AbcM-MFE0cdhb52g2N"

# Reference alphabet
alphabet = "!\"#$%&'()*+,-./0123456789:;<=>?@ABCDEFGHIJKLMNOPQRSTUVWXYZ"+ \
            "[\\]^_`abcdefghijklmnopqrstuvwxyz{|}~"



def decode_secret(secret):
    """ROT47 decode

    NOTE: encode and decode are the same operation in the ROT cipher family.
    """

    # Encryption key
    rotate_const = 47

    # Storage for decoded secret
    decoded = ""

    # decode loop
    for c in secret:
        index = alphabet.find(c)
        original_index = (index + rotate_const) % len(alphabet)
        decoded = decoded + alphabet[original_index]

    print(decoded)



def choose_greatest():
    """Echo the largest of the two numbers given by the user to the program

    Warning: this function was written quickly and needs proper error handling
    """

    user_value_1 = input("What's your first number? ")
    user_value_2 = input("What's your second number? ")
    greatest_value = user_value_1 # need a value to return if 1 & 2 are equal

    if user_value_1 > user_value_2:
        greatest_value = user_value_1
    elif user_value_1 < user_value_2:
        greatest_value = user_value_2

    print( "The number with largest positive magnitude is "
        + str(greatest_value) )



choose_greatest()
```

```bash
┌──(armando㉿kali)-[~/picoCTF/reversing/crackme-py]
└─$ nano crackme.py
```
- Modificamos el código para decodificar la contraseña.
```python
# Hiding this really important number in an obscure piece of code is brilliant!
# AND it's encrypted!
# We want our biggest client to know his information is safe with us.
bezos_cc_secret = "A:4@r%uL`M-^M0c0AbcM-MFE0cdhb52g2N"
# Reference alphabet
alphabet = "!\"#$%&'()*+,-./0123456789:;<=>?@ABCDEFGHIJKLMNOPQRSTUVWXYZ"+ \
            "[\\]^_`abcdefghijklmnopqrstuvwxyz{|}~"
def decode_secret(secret):
    """ROT47 decode
    
    NOTE: encode and decode are the same operation in the ROT cipher family.
    """
    # Encryption key
    rotate_const = 47
    # Storage for decoded secret
    decoded = ""
    # decode loop
    for c in secret:
        index = alphabet.find(c)
        original_index = (index + rotate_const) % len(alphabet)
        decoded = decoded + alphabet[original_index]
    print(decoded)
def choose_greatest():
    """Echo the largest of the two numbers given by the user to the program
    
    Warning: this function was written quickly and needs proper error handling
    """
    user_value_1 = input("What's your first number? ")
    user_value_2 = input("What's your second number? ")
    greatest_value = user_value_1 # need a value to return if 1 & 2 are equal
    if user_value_1 > user_value_2:
        greatest_value = user_value_1
    elif user_value_1 < user_value_2:
        greatest_value = user_value_2
    print( "The number with largest positive magnitude is "
        + str(greatest_value) )
#choose_greatest()
decode_secret(bezos_cc_secret)
```
- Y ya solo ejecutamos el programa.
```bash
┌──(armando㉿kali)-[~/picoCTF/reversing/crackme-py]
└─$ python3 crackme.py                                                                    
picoCTF{1|\/|_4_p34|\|ut_4593da8a}

┌──(armando㉿kali)-[~/picoCTF/reversing/crackme-py]
└─$ 
```

## Notas Adicionales
## Referencias