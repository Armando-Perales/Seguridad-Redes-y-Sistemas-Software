## Objetivo
The password for the next level can be retrieved by submitting the password of the current level to **port 30001 on localhost** using SSL/TLS encryption.

**Helpful note: Getting “DONE”, “RENEGOTIATING” or “KEYUPDATE”? Read the “CONNECTED COMMANDS” section in the manpage.**
## Datos de Acceso al Nivel
bandit15
8xCjnmgoKbGLhHFAZlGE5Tmu4M2tKJQo
## Solución
### Forma 1
```
bandit15@bandit:~$ ncat -v --ssl localhost 30001
Ncat: Version 7.94SVN ( https://nmap.org/ncat )
Ncat: Subject: CN=SnakeOil
Ncat: Issuer: CN=SnakeOil
Ncat: SHA-1 fingerprint: 323A F3B1 4FC7 1B0F F71A 1931 8FF3 62A1 49AC 735A
Ncat: Certificate verification failed (self-signed certificate).
Ncat: SSL connection to 127.0.0.1:30001.
Ncat: SHA-1 fingerprint: 323A F3B1 4FC7 1B0F F71A 1931 8FF3 62A1 49AC 735A
8xCjnmgoKbGLhHFAZlGE5Tmu4M2tKJQo
Correct!
kSkvUpMQ7lBYyCM4GBPvCvT1BfWRy0Dx
```
### Forma 2
```bash
bandit15@bandit:~$ openssl s_client -connect localhost:30001
CONNECTED(00000003)
Can't use SSL_get_servername
depth=0 CN = SnakeOil
verify error:num=18:self-signed certificate
verify return:1
depth=0 CN = SnakeOil
verify return:1
---
Certificate chain
 0 s:CN = SnakeOil
   i:CN = SnakeOil
   a:PKEY: rsaEncryption, 4096 (bit); sigalg: RSA-SHA256
   v:NotBefore: Jun 10 03:59:50 2024 GMT; NotAfter: Jun  8 03:59:50 2034 GMT
---
Server certificate
-----BEGIN CERTIFICATE-----
MIIFBzCCAu+gAwIBAgIUBLz7DBxA0IfojaL/WaJzE6Sbz7cwDQYJKoZIhvcNAQEL
BQAwEzERMA8GA1UEAwwIU25ha2VPaWwwHhcNMjQwNjEwMDM1OTUwWhcNMzQwNjA4
MDM1OTUwWjATMREwDwYDVQQDDAhTbmFrZU9pbDCCAiIwDQYJKoZIhvcNAQEBBQAD
ggIPADCCAgoCggIBANI+P5QXm9Bj21FIPsQqbqZRb5XmSZZJYaam7EIJ16Fxedf+
jXAv4d/FVqiEM4BuSNsNMeBMx2Gq0lAfN33h+RMTjRoMb8yBsZsC063MLfXCk4p+
09gtGP7BS6Iy5XdmfY/fPHvA3JDEScdlDDmd6Lsbdwhv93Q8M6POVO9sv4HuS4t/
jEjr+NhE+Bjr/wDbyg7GL71BP1WPZpQnRE4OzoSrt5+bZVLvODWUFwinB0fLaGRk
GmI0r5EUOUd7HpYyoIQbiNlePGfPpHRKnmdXTTEZEoxeWWAaM1VhPGqfrB/Pnca+
vAJX7iBOb3kHinmfVOScsG/YAUR94wSELeY+UlEWJaELVUntrJ5HeRDiTChiVQ++
wnnjNbepaW6shopybUF3XXfhIb4NvwLWpvoKFXVtcVjlOujF0snVvpE+MRT0wacy
tHtjZs7Ao7GYxDz6H8AdBLKJW67uQon37a4MI260ADFMS+2vEAbNSFP+f6ii5mrB
18cY64ZaF6oU8bjGK7BArDx56bRc3WFyuBIGWAFHEuB948BcshXY7baf5jjzPmgz
mq1zdRthQB31MOM2ii6vuTkheAvKfFf+llH4M9SnES4NSF2hj9NnHga9V08wfhYc
x0W6qu+S8HUdVF+V23yTvUNgz4Q+UoGs4sHSDEsIBFqNvInnpUmtNgcR2L5PAgMB
AAGjUzBRMB0GA1UdDgQWBBTPo8kfze4P9EgxNuyk7+xDGFtAYzAfBgNVHSMEGDAW
gBTPo8kfze4P9EgxNuyk7+xDGFtAYzAPBgNVHRMBAf8EBTADAQH/MA0GCSqGSIb3
DQEBCwUAA4ICAQAKHomtmcGqyiLnhziLe97Mq2+Sul5QgYVwfx/KYOXxv2T8ZmcR
Ae9XFhZT4jsAOUDK1OXx9aZgDGJHJLNEVTe9zWv1ONFfNxEBxQgP7hhmDBWdtj6d
taqEW/Jp06X+08BtnYK9NZsvDg2YRcvOHConeMjwvEL7tQK0m+GVyQfLYg6jnrhx
egH+abucTKxabFcWSE+Vk0uJYMqcbXvB4WNKz9vj4V5Hn7/DN4xIjFko+nREw6Oa
/AUFjNnO/FPjap+d68H1LdzMH3PSs+yjGid+6Zx9FCnt9qZydW13Miqg3nDnODXw
+Z682mQFjVlGPCA5ZOQbyMKY4tNazG2n8qy2famQT3+jF8Lb6a4NGbnpeWnLMkIu
jWLWIkA9MlbdNXuajiPNVyYIK9gdoBzbfaKwoOfSsLxEqlf8rio1GGcEV5Hlz5S2
txwI0xdW9MWeGWoiLbZSbRJH4TIBFFtoBG0LoEJi0C+UPwS8CDngJB4TyrZqEld3
rH87W+Et1t/Nepoc/Eoaux9PFp5VPXP+qwQGmhir/hv7OsgBhrkYuhkjxZ8+1uk7
tUWC/XM0mpLoxsq6vVl3AJaJe1ivdA9xLytsuG4iv02Juc593HXYR8yOpow0Eq2T
U5EyeuFg5RXYwAPi7ykw1PW7zAPL4MlonEVz+QXOSx6eyhimp1VZC11SCg==
-----END CERTIFICATE-----
subject=CN = SnakeOil
issuer=CN = SnakeOil
---
No client certificate CA names sent
Peer signing digest: SHA256
Peer signature type: RSA-PSS
Server Temp Key: X25519, 253 bits
---
SSL handshake has read 2103 bytes and written 373 bytes
Verification error: self-signed certificate
---
New, TLSv1.3, Cipher is TLS_AES_256_GCM_SHA384
Server public key is 4096 bit
Secure Renegotiation IS NOT supported
Compression: NONE
Expansion: NONE
No ALPN negotiated
Early data was not sent
Verify return code: 18 (self-signed certificate)
---
---
Post-Handshake New Session Ticket arrived:
SSL-Session:
    Protocol  : TLSv1.3
    Cipher    : TLS_AES_256_GCM_SHA384
    Session-ID: 2F455D9F50BF31AC3628C366D4571464D40425AD34383DEBC3528CB3D7970041
    Session-ID-ctx:
    Resumption PSK: 489A8E702709F06DA159BFDFF053A947C99055631E2BE98A6892E9AB0184A7E7BCAFF800CF4916B657FED0102BFF4BAA
    PSK identity: None
    PSK identity hint: None
    SRP username: None
    TLS session ticket lifetime hint: 300 (seconds)
    TLS session ticket:
    0000 - 43 87 d0 c4 a5 49 95 26-c8 3e eb 08 d7 47 78 ca   C....I.&.>...Gx.
    0010 - d0 65 38 fc fc 56 74 38-58 e6 d9 c3 33 86 1d b9   .e8..Vt8X...3...
    0020 - c8 29 25 e9 cf a5 77 77-e0 b8 e4 88 0f 24 02 64   .)%...ww.....$.d
    0030 - 1f 32 b4 42 09 2c d9 82-9d 12 4a de f2 18 a7 a5   .2.B.,....J.....
    0040 - 3a 92 58 67 53 3b 27 38-30 71 c6 d5 9b fd b5 5b   :.XgS;'80q.....[
    0050 - 6b 47 8d bb 42 78 a5 80-9c c2 1a a9 68 ec 06 d1   kG..Bx......h...
    0060 - 5f 56 bd 0f f7 f2 2d 43-b5 4e 4b 4e 19 32 0b cc   _V....-C.NKN.2..
    0070 - 4d 47 89 e1 14 07 55 a5-e5 49 1b 0e 86 7d 63 47   MG....U..I...}cG
    0080 - 24 d5 57 bd d8 5a 42 56-8c db 42 b8 af cd 1c 47   $.W..ZBV..B....G
    0090 - 1a 33 d3 f1 54 e2 ee b3-6f 96 86 76 c7 0e 9b b1   .3..T...o..v....
    00a0 - 26 7b f5 cb db f8 67 6f-aa 3a ab b4 98 63 b4 73   &{....go.:...c.s
    00b0 - bf e5 e4 7a 77 e5 42 5e-6c 02 1d dc ca ef 0c 9a   ...zw.B^l.......
    00c0 - 0c e5 9e 6e 41 7a be 9a-3e b2 63 2d e8 25 8e 4a   ...nAz..>.c-.%.J
    00d0 - 70 f1 52 af df c7 90 5e-84 ef 43 5a 20 a6 08 e1   p.R....^..CZ ...

    Start Time: 1724868927
    Timeout   : 7200 (sec)
    Verify return code: 18 (self-signed certificate)
    Extended master secret: no
    Max Early Data: 0
---
read R BLOCK
---
Post-Handshake New Session Ticket arrived:
SSL-Session:
    Protocol  : TLSv1.3
    Cipher    : TLS_AES_256_GCM_SHA384
    Session-ID: 4928CFCB3102ED1D24B8BCE3FC926F3830E2841F876025444FE6791650BB973F
    Session-ID-ctx:
    Resumption PSK: 41DCD95A86841160E8CF592D2C95BBF734941DB5D2BC9A692EF855E5F745F9655166DE495C470C173DE1F286596A9F0B
    PSK identity: None
    PSK identity hint: None
    SRP username: None
    TLS session ticket lifetime hint: 300 (seconds)
    TLS session ticket:
    0000 - 43 87 d0 c4 a5 49 95 26-c8 3e eb 08 d7 47 78 ca   C....I.&.>...Gx.
    0010 - 3d 3a 31 6f ac 4c d6 77-8f 44 4f f9 6f c7 7f 90   =:1o.L.w.DO.o...
    0020 - f9 e2 5b 9c 5f 31 02 5c-04 5b 74 b2 f6 3b 55 ca   ..[._1.\.[t..;U.
    0030 - 4d d0 46 62 c3 14 fc eb-03 3e 24 7b 5f 62 8c 24   M.Fb.....>${_b.$
    0040 - 2f 73 fc aa cb ec be 2f-9e 34 25 1f 0e ed dd 08   /s...../.4%.....
    0050 - d5 36 e9 a8 5b 69 39 f4-fa f5 ec d5 a8 35 b5 fa   .6..[i9......5..
    0060 - 25 33 23 2d 5c a4 3a 1d-2f 95 69 75 ba 43 f7 5f   %3#-\.:./.iu.C._
    0070 - a8 df 81 d5 19 b3 3c bc-bc 92 23 77 64 75 39 26   ......<...#wdu9&
    0080 - bf 6a 40 6b d1 be 0a 23-84 c6 be 60 78 93 3e 1d   .j@k...#...`x.>.
    0090 - 01 ea 61 ae d1 93 01 6f-4d a2 bb cd 85 9e 16 5b   ..a....oM......[
    00a0 - ab c1 32 0b d4 80 c7 4c-5a 84 9f 82 d3 ef 65 a5   ..2....LZ.....e.
    00b0 - fe e9 cf 22 c3 1a 76 5a-c3 fc 76 49 b5 88 88 84   ..."..vZ..vI....
    00c0 - ca 67 05 a5 c9 64 fa be-d3 fc eb ff 36 3a 8a b9   .g...d......6:..
    00d0 - b5 2a e9 3d 34 b1 10 1c-32 a5 ea cf 13 2f d2 01   .*.=4...2..../..

    Start Time: 1724868927
    Timeout   : 7200 (sec)
    Verify return code: 18 (self-signed certificate)
    Extended master secret: no
    Max Early Data: 0
---
read R BLOCK
8xCjnmgoKbGLhHFAZlGE5Tmu4M2tKJQo
Correct!
kSkvUpMQ7lBYyCM4GBPvCvT1BfWRy0Dx

closed
bandit15@bandit:~$
```
## Notas Adicionales
ssl/tsl - es un protocolo de comunicación generalmente usado en sitios web (https)
ncat - es una herramienta similar a netcat, pero con otras ventajas como conectar puertos ssl
openssl - 
openssl s_client -connect localhost:30001
	openssl - Es una herramienta de línea de comandos que forma parte de la suite OpenSSL, la cual se utiliza para trabajar con criptografía, incluyendo la creación de claves y certificados, y el establecimiento de conexiones seguras utilizando SSL/TLS
	s_client - Permite establecer una conexión SSL/TLS con un servidor y es útil para probar y depurar la configuración de seguridad del servidor
	-connect - Es un indicador que le dice a qué servidor y puerto debe conectarse
	localhost - es el host o la maquina a la que me quiero conectar
	30001 - es el puerto que esta abierto en esa maquina
## Referencias
- [Secure Socket Layer/Transport Layer Security on Wikipedia](https://en.wikipedia.org/wiki/Transport_Layer_Security)
- [OpenSSL Cookbook - Testing with OpenSSL](https://www.feistyduck.com/library/openssl-cookbook/online/testing-with-openssl/index.html)