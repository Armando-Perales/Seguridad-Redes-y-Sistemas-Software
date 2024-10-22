## Objetivo
We have several pages hidden. Can you find the one with the flag?The website is running [here](http://saturn.picoctf.net:58210/).
## Solución
- Entramos al código fuente de la pagina.
```html
<!DOCTYPE html>
<html>
  <head>
    <meta charset="UTF-8" />
    <meta
      name="viewport"
      content="width=device-width, initial-scale=1, shrink-to-fit=no"
    />
    <meta name="description" content="" />
    <!-- Bootstrap core CSS -->
    <link href="vendor/bootstrap/css/bootstrap.min.css" rel="stylesheet" />
    <!-- title -->
    <title>home</title>
    <!-- css -->
    <link href="secret/assets/index.css" rel="stylesheet" />
  </head>
  <body>
    <!-- ***** Header Area Start ***** -->
    <div class="topnav">
      <a class="active" href="#home">Home</a>
      <a href="about.html">About</a>
      <a href="contact.html">Contact</a>
    </div>

    <div class="imgcontainer">
      <img
        src="secret/assets/DX1KYM.jpg"
        alt="https://www.alamy.com/security-safety-word-cloud-concept-image-image67649784.html"
        class="responsive"
      />
      <div class="top-left">
        <h1>If security wasn't your job, would you do it as a hobby?</h1>
      </div>
    </div>
  </body>
</html>
```
- Entramos a la carpeta llamada `secret` ya que es lo que estamos buscando (el secreto que esconde la pagina) y vemos el código fuente de la carpeta.
```bash
http://saturn.picoctf.net:58210/secret/
```

```html

<!DOCTYPE html>
<html>
  <head>
    <title></title>
    <link rel="stylesheet" href="hidden/file.css" />
  </head>

  <body>
    <h1>Finally. You almost found me. you are doing well</h1>
    <img src="https://media1.tenor.com/images/0a6aff9f825af62c05adfbd75039cc7b/tenor.gif?itemid=4648337" alt="Something Like That GIF - Andy Parksandrecreation Wtf GIFs" style="max-width: 833px; background-color: rgb(151, 121, 85);" width="833" height="937.125">
  </body>
</html>

```
- De aquí entramos a la carpeta llamada `hidden` para ver que esconde.
```bash
http://saturn.picoctf.net:62412/secret/hidden/
```

```html
<!DOCTYPE html>
<html>
  <head>
    <title>LOGIN</title>
    <!-- css -->
    <link href="superhidden/login.css" rel="stylesheet" />
  </head>
  <body>
    <form>
      <div class="container">
        <form method="" action="/secret/assets/popup.js">
          <div class="row">
            <h2 style="text-align: center">
              Login with Social Media or Manually
            </h2>
            <div class="vl">
              <span class="vl-innertext">or</span>
            </div>

            <div class="col">
              <a href="#" class="fb btn">
                <i class="fa fa-facebook fa-fw"></i> Login with Facebook
              </a>
              <a href="#" class="twitter btn">
                <i class="fa fa-twitter fa-fw"></i> Login with Twitter
              </a>
              <a href="#" class="google btn">
                <i class="fa fa-google fa-fw"></i> Login with Google+
              </a>
            </div>

            <div class="col">
              <div class="hide-md-lg">
                <p>Or sign in manually:</p>
              </div>

              <input
                type="text"
                name="username"
                placeholder="Username"
                required
              />
              <input
                type="password"
                name="password"
                placeholder="Password"
                required
              />
              <input type="hidden" name="db" value="superhidden/xdfgwd.html" />

              <input
                type="submit"
                value="Login"
                onclick="alert('Thank you for the attempt but oops! try harder. better luck next time')"
              />
            </div>
          </div>
        </form>
      </div>

      <div class="bottom-container">
        <div class="row">
          <div class="col">
            <a href="#" style="color: white" class="btn">Sign up</a>
          </div>
          <div class="col">
            <a href="#" style="color: white" class="btn">Forgot password?</a>
          </div>
        </div>
      </div>
    </form>
  </body>
</html>
```
- Ahora nos vamos a la carpeta llamada `superhidden` para encontrar la bandera.
```bash
http://saturn.picoctf.net:62412/secret/hidden/superhidden/
```

```html
<!DOCTYPE html>
<html>
  <head>
    <title></title>
    <link rel="stylesheet" href="mycss.css" />
  </head>

  <body>
    <h1>Finally. You found me. But can you see me</h1>
    <h3 class="flag">picoCTF{succ3ss_@h3n1c@10n_51b260fe}</h3>
  </body>
</html>
```

## Notas Adicionales
## Referencias