## Objetivo
[keygenme-trial.py](https://mercury.picoctf.net/static/0c363291c47477642c72630d68936e50/keygenme-trial.py)
## Solución

```bash
┌──(armando㉿kali)-[~/picoCTF/reversing/keygenme-py]
└─$ ls
keygenme-trial.py

┌──(armando㉿kali)-[~/picoCTF/reversing/keygenme-py]
└─$ nano keygenme-trial.py
```
- Revisamos el programa de Python que nos dan.
```python
#============================================================================#
#============================ARCANE CALCULATOR===============================#
#============================================================================#

import hashlib
from cryptography.fernet import Fernet
import base64



# GLOBALS --v
arcane_loop_trial = True
jump_into_full = False
full_version_code = ""

username_trial = "MORTON"
bUsername_trial = b"MORTON"

key_part_static1_trial = "picoCTF{1n_7h3_|<3y_of_"
key_part_dynamic1_trial = "xxxxxxxx"
key_part_static2_trial = "}"
key_full_template_trial = key_part_static1_trial + key_part_dynamic1_trial + key_part_static2_trial

star_db_trial = {
  "Alpha Centauri": 4.38,
  "Barnard's Star": 5.95,
  "Luhman 16": 6.57,
  "WISE 0855-0714": 7.17,
  "Wolf 359": 7.78,
  "Lalande 21185": 8.29,
  "UV Ceti": 8.58,
  "Sirius": 8.59,
  "Ross 154": 9.69,
  "Yin Sector CL-Y d127": 9.86,
  "Duamta": 9.88,
  "Ross 248": 10.37,
  "WISE 1506+7027": 10.52,
  "Epsilon Eridani": 10.52,
  "Lacaille 9352": 10.69,
  "Ross 128": 10.94,
  "EZ Aquarii": 11.10,
  "61 Cygni": 11.37,
  "Procyon": 11.41,
  "Struve 2398": 11.64,
  "Groombridge 34": 11.73,
  "Epsilon Indi": 11.80,
  "SPF-LF 1": 11.82,
  "Tau Ceti": 11.94,
  "YZ Ceti": 12.07,
  "WISE 0350-5658": 12.09,
  "Luyten's Star": 12.39,
  "Teegarden's Star": 12.43,
  "Kapteyn's Star": 12.76,
  "Talta": 12.83,
  "Lacaille 8760": 12.88
}

 
def intro_trial():
    print("\n===============================================\n\
Welcome to the Arcane Calculator, " + username_trial + "!\n")    
    print("This is the trial version of Arcane Calculator.")
    print("The full version may be purchased in person near\n\
the galactic center of the Milky Way galaxy. \n\
Available while supplies last!\n\
=====================================================\n\n")


def menu_trial():
    print("___Arcane Calculator___\n\n\
Menu:\n\
(a) Estimate Astral Projection Mana Burn\n\
(b) [LOCKED] Estimate Astral Slingshot Approach Vector\n\
(c) Enter License Key\n\
(d) Exit Arcane Calculator")

    choice = input("What would you like to do, "+ username_trial +" (a/b/c/d)? ")
    
    if not validate_choice(choice):
        print("\n\nInvalid choice!\n\n")
        return
    
    if choice == "a":
        estimate_burn()
    elif choice == "b":
        locked_estimate_vector()
    elif choice == "c":
        enter_license()
    elif choice == "d":
        global arcane_loop_trial
        arcane_loop_trial = False
        print("Bye!")
    else:
        print("That choice is not valid. Please enter a single, valid \
lowercase letter choice (a/b/c/d).")


def validate_choice(menu_choice):
    if menu_choice == "a" or \
       menu_choice == "b" or \
       menu_choice == "c" or \
       menu_choice == "d":
        return True
    else:
        return False


def estimate_burn():
  print("\n\nSOL is detected as your nearest star.")
  target_system = input("To which system do you want to travel? ")

  if target_system in star_db_trial:
      ly = star_db_trial[target_system]
      mana_cost_low = ly**2
      mana_cost_high = ly**3
      print("\n"+ target_system +" will cost between "+ str(mana_cost_low) \
+" and "+ str(mana_cost_high) +" stone(s) to project to\n\n")
  else:
      # TODO : could add option to list known stars
      print("\nStar not found.\n\n")


def locked_estimate_vector():
    print("\n\nYou must buy the full version of this software to use this \
feature!\n\n")


def enter_license():
    user_key = input("\nEnter your license key: ")
    user_key = user_key.strip()

    global bUsername_trial
    
    if check_key(user_key, bUsername_trial):
        decrypt_full_version(user_key)
    else:
        print("\nKey is NOT VALID. Check your data entry.\n\n")


def check_key(key, username_trial):

    global key_full_template_trial

    if len(key) != len(key_full_template_trial):
        return False
    else:
        # Check static base key part --v
        i = 0
        for c in key_part_static1_trial:
            if key[i] != c:
                return False

            i += 1
        # TODO : test performance on toolbox container
        # Check dynamic part --v
        if key[i] != hashlib.sha256(username_trial).hexdigest()[4]:
            return False
        else:
            i += 1

        if key[i] != hashlib.sha256(username_trial).hexdigest()[5]:
            return False
        else:
            i += 1

        if key[i] != hashlib.sha256(username_trial).hexdigest()[3]:
            return False
        else:
            i += 1

        if key[i] != hashlib.sha256(username_trial).hexdigest()[6]:
            return False
        else:
            i += 1

        if key[i] != hashlib.sha256(username_trial).hexdigest()[2]:
            return False
        else:
            i += 1

        if key[i] != hashlib.sha256(username_trial).hexdigest()[7]:
            return False
        else:
            i += 1

        if key[i] != hashlib.sha256(username_trial).hexdigest()[1]:
            return False
        else:
            i += 1

        if key[i] != hashlib.sha256(username_trial).hexdigest()[8]:
            return False



        return True


def decrypt_full_version(key_str):

    key_base64 = base64.b64encode(key_str.encode())
    f = Fernet(key_base64)

    try:
        with open("keygenme.py", "w") as fout:
          global full_version
          global full_version_code
          full_version_code = f.decrypt(full_version)
          fout.write(full_version_code.decode())
          global arcane_loop_trial
          arcane_loop_trial = False
          global jump_into_full
          jump_into_full = True
          print("\nFull version written to 'keygenme.py'.\n\n"+ \
                 "Exiting trial version...")
    except FileExistsError:
        sys.stderr.write("Full version of keygenme NOT written to disk, "+ \
                          "ERROR: 'keygenme.py' file already exists.\n\n"+ \
                          "ADVICE: If this existing file is not valid, "+ \
                          "you may try deleting it and entering the "+ \
                          "license key again. Good luck")

def ui_flow():
    intro_trial()
    while arcane_loop_trial:
        menu_trial()



# Encrypted blob of full version
full_version = \
b"""
gAAAAABgT_nv3JrW2AMPOanzoOatT8tWrZSH9V2-H_-sY8RFTh1Vr9guvCw3iIUq7eVs4IhR2u6bI_HkJm6u5VK99vYIKXfthUYjQRMNmo6uMwqdK8Z>
"""



# Enter main loop
ui_flow()

if jump_into_full:
    exec(full_version_code)
```

```bash
┌──(armando㉿kali)-[~/picoCTF/reversing/keygenme-py]
└─$ nano solve.py
```
- Creamos un programa en Python para que nos de la parte dinámica de la bandera.
```python
import hashlib
import base64


key_part_static1_trial = "picoCTF{1n_7h3_|<3y_of_"
key_part_dynamic1_trial = "xxxxxxxx"
key_part_static2_trial = "}"
key_full_template_trial = key_part_static1_trial + key_part_dynamic1_trial + key_part_static2_trial

username_trial = b"MORTON"

potential_dynamic_key = ""

offset = 23

positions = [4,5,3,6,2,7,1,8]

for p in positions:
    potential_dynamic_key += hashlib.sha256(username_trial).hexdigest()[p]

key = key_part_static1_trial + potential_dynamic_key + key_part_static2_trial
print(key)
print(len(key))
```
- Ejecutamos el programa y obtenemos la bandera.
```bash
┌──(armando㉿kali)-[~/picoCTF/reversing/keygenme-py]
└─$ python3 solve.py
picoCTF{1n_7h3_|<3y_of_75fc1081}
32

┌──(armando㉿kali)-[~/picoCTF/reversing/keygenme-py]
└─$
```

## Notas Adicionales
## Referencias