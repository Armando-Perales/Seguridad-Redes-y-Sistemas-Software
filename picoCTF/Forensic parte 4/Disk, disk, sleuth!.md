## Objetivo
Use `srch_strings` from the sleuthkit and some terminal-fu to find a flag in this disk image: [dds1-alpine.flag.img.gz](https://mercury.picoctf.net/static/f63e4eba644c99e92324b65cbd875db6/dds1-alpine.flag.img.gz)
## Solución
- Instalamos las herramientas Sleuth Kit y Autopsy.
```bash
┌──(armando㉿kali)-[~/picoCTF/forensic/diskdisksleuth]
└─$ sudo apt install sleuthkit                                                                         
...

┌──(armando㉿kali)-[~/picoCTF/forensic/diskdisksleuth]
└─$ sudo apt install autopsy  

...

┌──(armando㉿kali)-[~/picoCTF/forensic/diskdisksleuth]
└─$ file dds1-alpine.flag.img.gz 
dds1-alpine.flag.img.gz: gzip compressed data, was "dds1-alpine.flag.img", last modified: Tue Mar 16 00:19:51 2021, from Unix, original size modulo 2^32 134217728
```
- Descomprimimos el archivo.
```bash
┌──(armando㉿kali)-[~/picoCTF/forensic/diskdisksleuth]
└─$ gzip -d dds1-alpine.flag.img.gz            

┌──(armando㉿kali)-[~/picoCTF/forensic/diskdisksleuth]
└─$ file dds1-alpine.flag.img   
dds1-alpine.flag.img: DOS/MBR boot sector; partition 1 : ID=0x83, active, start-CHS (0x0,32,33), end-CHS (0x10,81,1), startsector 2048, 260096 sectors

┌──(armando㉿kali)-[~/picoCTF/forensic/diskdisksleuth]
└─$ mmls dds1-alpine.flag.img 
DOS Partition Table
Offset Sector: 0
Units are in 512-byte sectors

      Slot      Start        End          Length       Description
000:  Meta      0000000000   0000000000   0000000001   Primary Table (#0)
001:  -------   0000000000   0000002047   0000002048   Unallocated
002:  000:000   0000002048   0000262143   0000260096   Linux (0x83)

┌──(armando㉿kali)-[~/picoCTF/forensic/diskdisksleuth]
└─$ srch_strings dds1-alpine.flag.img | grep pico
ffffffff81399ccf t pirq_pico_get
ffffffff81399cee t pirq_pico_set
ffffffff820adb46 t pico_router_probe
  SAY picoCTF{f0r3ns1c4t0r_n30phyt3_ad5c96c0}

┌──(armando㉿kali)-[~/picoCTF/forensic/diskdisksleuth]
└─$ 
```

## Notas Adicionales
mmls - nos da información de las particiones.
srch_string - busca cadenas.
## Referencias
