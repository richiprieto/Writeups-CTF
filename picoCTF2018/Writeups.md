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
