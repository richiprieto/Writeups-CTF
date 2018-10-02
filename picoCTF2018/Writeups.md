# Writeups de picoCTF2018

## admin panel - Points: 150

Nos solicita que encontremos el password del admin

![alt text](https://github.com/richiprieto/Writeups-CTF/blob/master/picoCTF2018/imagenes/adminpanel.png)

Lo que hacemos es abrir el archivo con Wireshark, el cual nos permite ver los paquetes que han sido capturados, encontramos un paquete que contiene un login mediante post

![alt text](https://github.com/richiprieto/Writeups-CTF/blob/master/picoCTF2018/imagenes/adminpanel1.png)

Buscando dentro del paquete encontramos al final el flag del reto en el campo password

![alt text](https://github.com/richiprieto/Writeups-CTF/blob/master/picoCTF2018/imagenes/adminpanel2.png)

## Store - Points: 400

Debemos encontrar la flag que se encuentra dentro del archivo store que nos es proporcionado

![alt text](https://github.com/richiprieto/Writeups-CTF/blob/master/picoCTF2018/imagenes/store.png)

Descargamos el archivo y aplicamos el comando **strings store** para ver las strings que contiene

![alt text](https://github.com/richiprieto/Writeups-CTF/blob/master/picoCTF2018/imagenes/store1.png)

Revisando los strings que contiene observamos la flag que necesitamos :D

![alt text](https://github.com/richiprieto/Writeups-CTF/blob/master/picoCTF2018/imagenes/store2.png)

## No Login - Points: 200

Nos dice que la flag solo se la entrega al admin.

![alt text](https://github.com/richiprieto/Writeups-CTF/blob/master/picoCTF2018/imagenes/nologin.png)

Al ingresar tenemos un boton que dice flag, pero al no ser administradores nos sale un aviso que no somos administradores y por lo tanto no tenemos acceso al mismo.

![alt text](https://github.com/richiprieto/Writeups-CTF/blob/master/picoCTF2018/imagenes/nologin1.png)

Usando la herramienta [Burp Suite](https://portswigger.net/burp) interceptamos la comunicacion del requerimiento

![alt text](https://github.com/richiprieto/Writeups-CTF/blob/master/picoCTF2018/imagenes/nologin2.png)

Una vez interceptada agregamos en el campo cookie el parametro **admin=True** para que la cookie nos diga que somos administradores

![alt text](https://github.com/richiprieto/Writeups-CTF/blob/master/picoCTF2018/imagenes/nologin3.png)

Una vez hecho eso nuestra cookie deberia quedar de la siguiente manera, notar que se agregó el campo admin

![alt text](https://github.com/richiprieto/Writeups-CTF/blob/master/picoCTF2018/imagenes/nologin4.png)

Al enviar la petición modificada dando click en el botón forward nos aparece la flag en la pagina

![alt text](https://github.com/richiprieto/Writeups-CTF/blob/master/picoCTF2018/imagenes/nologin5.png)
