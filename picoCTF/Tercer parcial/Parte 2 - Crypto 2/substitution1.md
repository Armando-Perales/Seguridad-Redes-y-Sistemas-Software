## Objetivo
A second message has come in the mail, and it seems almost identical to the first one. Maybe the same thing will work again. Download the message [here](https://artifacts.picoctf.net/c/181/message.txt).
## Solución
- Nos dan el siguiente texto.
```bash
┌──(armando㉿kali)-[~/picoCTF/crypto/substitution1]
└─$ ls
message.txt

┌──(armando㉿kali)-[~/picoCTF/crypto/substitution1]
└─$ cat message.txt 
ZWDg (gejfw djf zacwpfx wex dqar) afx a wscx jd zjicpwxf gxzpfbws zjicxwbwbjv. Zjvwxgwavwg afx cfxgxvwxm hbwe a gxw jd zeaqqxvrxg hebze wxgw wexbf zfxawbybws, wxzevbzaq (avm rjjrqbvr) gnbqqg, avm cfjtqxi-gjqybvr atbqbws. Zeaqqxvrxg pgpaqqs zjyxf a vpitxf jd zawxrjfbxg, avm hexv gjqyxm, xaze sbxqmg a gwfbvr (zaqqxm a dqar) hebze bg gptibwwxm wj av jvqbvx gzjfbvr gxfybzx. ZWDg afx a rfxaw has wj qxafv a hbmx affas jd zjicpwxf gxzpfbws gnbqqg bv a gadx, qxraq xvybfjvixvw, avm afx ejgwxm avm cqasxm ts iavs gxzpfbws rfjpcg afjpvm wex hjfqm djf dpv avm cfazwbzx. Djf webg cfjtqxi, wex dqar bg: cbzjZWD{DF3LP3VZS_4774ZN5_4F3_Z001_4871X6DT}                                                                                                                    
┌──(armando㉿kali)-[~/picoCTF/crypto/substitution1]
└─$ 
```
- Con la ayuda de la siguiente pagina [Substitution Solver](https://www.guballa.de/substitution-solver) rompemos el cifrado.
```bash
CTFs (short for capture the flag) are a type of computer security competition. Contestants are presented with a set of challenges which test their creativity, technical (and googling) skills, and problem-solving ability. Challenges usually cover a number of categories, and when solved, each yields a string (called a flag) which is submitted to an online scoring service. CTFs are a great way to learn a wide array of computer security skills in a safe, legal environment, and are hosted and played by many security groups around the world for fun and practice. For this problem, the flag is: picoCTF{FR3JU3NCY_4774CK5_4R3_C001_4871E6FB}
```
- Es posible que marque error si le pasamos la bandera una vez desencriptado el mensaje, pero solo necesitamos cambiar una letra de la bandera.
```bash
picoCTF{FR3QU3NCY_4774CK5_4R3_C001_4871E6FB}
```

## Notas Adicionales
## Referencias
