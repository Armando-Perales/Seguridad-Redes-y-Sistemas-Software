## Objetivo
'Suspicious' is written all over this disk image. Download [suspicious.dd.sda1](https://jupiter.challenges.picoctf.org/static/7d5935462933be5b7f4811098bed9f74/suspicious.dd.sda1)
## Solución
```bash
┌──(armando㉿kali)-[~/picoCTF/forensic/pitterpatterplatters]
└─$ ls
suspicious.dd.sda1

┌──(armando㉿kali)-[~/picoCTF/forensic/pitterpatterplatters]
└─$ file suspicious.dd.sda1               
suspicious.dd.sda1: Linux rev 1.0 ext3 filesystem data, UUID=fc168af0-183b-4e53-bdf3-9c1055413b40 (needs journal recovery)

┌──(armando㉿kali)-[~/picoCTF/forensic/pitterpatterplatters]
└─$ fls suspicious.dd.sda1                
d/d 11: lost+found
d/d 2009:       boot
d/d 4017:       tce
r/r 12: suspicious-file.txt
V/V 8033:       $OrphanFiles

┌──(armando㉿kali)-[~/picoCTF/forensic/pitterpatterplatters]
└─$ icat suspicious.dd.sda1 12             
Nothing to see here! But you may want to look here -->

┌──(armando㉿kali)-[~/picoCTF/forensic/pitterpatterplatters]
└─$ xxd -s 0x200400 -l 200 suspicious.dd.sda1 
00200400: 4e6f 7468 696e 6720 746f 2073 6565 2068  Nothing to see h
00200410: 6572 6521 2042 7574 2079 6f75 206d 6179  ere! But you may
00200420: 2077 616e 7420 746f 206c 6f6f 6b20 6865   want to look he
00200430: 7265 202d 2d3e 0a7d 0036 0062 0037 0064  re -->.}.6.b.7.d
00200440: 0035 0034 0039 0062 005f 0033 003c 005f  .5.4.9.b._.3.<._
00200450: 007c 004c 006d 005f 0031 0031 0031 0074  .|.L.m._.1.1.1.t
00200460: 0035 005f 0033 0062 007b 0046 0054 0043  .5._.3.b.{.F.T.C
00200470: 006f 0063 0069 0070 0000 0000 0000 0000  .o.c.i.p........
00200480: 0000 0000 0000 0000 0000 0000 0000 0000  ................
00200490: 0000 0000 0000 0000 0000 0000 0000 0000  ................
002004a0: 0000 0000 0000 0000 0000 0000 0000 0000  ................
002004b0: 0000 0000 0000 0000 0000 0000 0000 0000  ................
002004c0: 0000 0000 0000 0000                      ........

┌──(armando㉿kali)-[~/picoCTF/forensic/pitterpatterplatters]
└─$ 
```
- Ahora con ayuda de CyberChef le colocamos el texto y le aplicamos 2 opciones `Reverse` y `Remove whitespace` marcando las opciones `Tabs`, `From feeds` y `Full stop`.
```bash
}.6.b.7.d.5.4.9.b._.3.<._.|.L.m._.1.1.1.t.5._.3.b.{.F.T.C.o.c.i.p.
```

```bash
picoCTF{b3_5t111_mL|_<3_b945d7b6}
```

## Notas Adicionales
## Referencias