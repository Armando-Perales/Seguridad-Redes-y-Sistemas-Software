## Objetivo
Attackers have hidden information in a very large mass of data in the past, maybe they are still doing it.Download the data [here](https://artifacts.picoctf.net/c/126/anthem.flag.txt).
## Solución
```bash
┌──(armando㉿kali)-[~/picoCTF/forensic/lookeyhere]
└─$ ls
anthem.flag.txt
                                                                                                                
┌──(armando㉿kali)-[~/picoCTF/forensic/lookeyhere]
└─$ cat anthem.flag.txt       
      ANTHEM

      by Ayn Rand


        CONTENTS

         PART ONE

         PART TWO

         PART THREE

         PART FOUR

         PART FIVE

         PART SIX

         PART SEVEN

         PART EIGHT

         PART NINE

         PART TEN

         PART ELEVEN

         PART TWELVE




      PART ONE
      
      ...
      
┌──(armando㉿kali)-[~/picoCTF/forensic/lookeyhere]
└─$ cat anthem.flag.txt | grep pico
      we think that the men of picoCTF{gr3p_15_@w3s0m3_2116b979}
    
┌──(armando㉿kali)-[~/picoCTF/forensic/lookeyhere]
└─$ 
```

## Notas Adicionales
## Referencias