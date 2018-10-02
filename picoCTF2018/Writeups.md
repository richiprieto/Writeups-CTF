# Algunos writeups del CTF picoCTF

## admin panel - Points: 150
Nos solicita que encontremos el password del admin
![alt text](https://github.com/richiprieto/Writeups-CTF/blob/master/picoCTF2018/imagenes/adminpanel.png)

Lo que hacemos es abrir el archivo con Wireshark, el cual nos permite ver los paquetes que han sido capturados, encontramos un paquete que contiene un login mediante post

![alt text](https://github.com/richiprieto/Writeups-CTF/blob/master/picoCTF2018/imagenes/adminpanel1.png)

Buscando dentro del paquete encontramos al final el flag del reto en el campo password

![alt text](https://github.com/richiprieto/Writeups-CTF/blob/master/picoCTF2018/imagenes/adminpanel2.png)
