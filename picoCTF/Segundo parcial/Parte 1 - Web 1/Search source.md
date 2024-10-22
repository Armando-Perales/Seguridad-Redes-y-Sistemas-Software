## Objetivo
The developer of this website mistakenly left an important artifact in the website source, can you find it?The website is [here](http://saturn.picoctf.net:54615/)
## Solución

```bash
┌──(armando㉿kali)-[~/picoCTF/web/searchsource]
└─$ httrack 'http://saturn.picoctf.net:54615/' 
Mirror launched on Sun, 20 Oct 2024 20:00:57 by HTTrack Website Copier/3.49-5 [XR&CO'2014]
mirroring http://saturn.picoctf.net:54615/ with the wizard help..
Done.: saturn.picoctf.net:54615/images/fevicon.png (153 bytes) - 404
Thanks for using HTTrack!

┌──(armando㉿kali)-[~/picoCTF/web/searchsource]
└─$ grep -nr picoCTF                    
saturn.picoctf.net_54615/css/style.css:328:/** banner_main picoCTF{1nsp3ti0n_0f_w3bpag3s_587d12b8} **/

┌──(armando㉿kali)-[~/picoCTF/web/searchsource]
└─$ 
```

## Notas Adicionales
## Referencias