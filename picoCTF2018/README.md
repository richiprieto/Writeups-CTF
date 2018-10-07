# Writeups de picoCTF2018

## admin panel - Points: 150

Nos solicita que encontremos el password del admin

![alt text](https://github.com/richiprieto/Writeups-CTF/blob/master/picoCTF2018/imagenes/adminpanel.png)

Lo que hacemos es abrir el archivo con [Wireshark](https://www.wireshark.org/), el cual nos permite ver los paquetes que han sido capturados, encontramos un paquete que contiene un login mediante post

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

## Recovering From the Snap - Points: 150

Al leer el reto como tal no encontraba la pista de como debia proceder, pero al momento de leer el hint me di cuenta que decia que algunos archivos fueron borrados, inmediatamente supuse que debia recuperarlos de la imagen que nos proporcionan llamado animals.

![alt text](https://github.com/richiprieto/Writeups-CTF/blob/master/picoCTF2018/imagenes/rfs.png)
![alt text](https://github.com/richiprieto/Writeups-CTF/blob/master/picoCTF2018/imagenes/rfs1.png)

Luego de descargar la imagen del disco lo primero que procede es montar el disco, para hacerlo utilice el siguiente comando

![alt text](https://github.com/richiprieto/Writeups-CTF/blob/master/picoCTF2018/imagenes/rfs2.png)

Para verificar el filesystem del archivo se utiliza el comando **df -hT** como podemos observar al ultimo en **/dev/loop0** esta el archivo montado animals

![alt text](https://github.com/richiprieto/Writeups-CTF/blob/master/picoCTF2018/imagenes/rfs3.png)

Despues de leer, encontre la herramienta [Foremost](https://tools.kali.org/forensics/foremost) para recuperar los archivos utilice los siguientes parametros **-v modo verboso, -q para habilitar el modo rápido, -t para el typo (en este caso todo "all") -i donde se especifica el input file, -o la carpeta de salida**

![alt text](https://github.com/richiprieto/Writeups-CTF/blob/master/picoCTF2018/imagenes/rfs4.png)

Luego de ejecutar vamos a la carpeta output y vemos entre varios archivos de animales el archivo que nos interesa

![alt text](https://github.com/richiprieto/Writeups-CTF/blob/master/picoCTF2018/imagenes/rfs5.png)

Finalmente obtenemos la flag, personalmente me agrado mucho debido a que en ningún anterior ctf me habian solicitado recuperar archivos para encontrar la tan deseada recompensa.

![alt text](https://github.com/richiprieto/Writeups-CTF/blob/master/picoCTF2018/imagenes/rfs6.png)

## The Vault - Points: 250

En el ejercicio The Vault nos piden loguearnos en una pagina web, no tenemos ningun hint

![alt text](https://github.com/richiprieto/Writeups-CTF/blob/master/picoCTF2018/imagenes/vault.png)

En la pagina web nos da un login y además el codigo en php de la pagina

![alt text](https://github.com/richiprieto/Writeups-CTF/blob/master/picoCTF2018/imagenes/vault1.png)

Intentamos con el user admin y password admin y observamos que hace una consulta directa al SQL

![alt text](https://github.com/richiprieto/Writeups-CTF/blob/master/picoCTF2018/imagenes/vault2.png)

Por lo que procedemos a intentar un sqlinjection **'or '1'='1** pero nos dice que fue detectado un intento de sql injection

![alt text](https://github.com/richiprieto/Writeups-CTF/blob/master/picoCTF2018/imagenes/vault3.png)

Revisando el codigo php nos damos cuenta que solo tiene validacion para el campo username por lo que intentamos el sql injection en el campo password

![alt text](https://github.com/richiprieto/Writeups-CTF/blob/master/picoCTF2018/imagenes/vault4.png)

Genial!!! colocando en el campo username cualquier valor y en el campo password el sqli **'or '1'='1**  obtenemos nuestra flag

![alt text](https://github.com/richiprieto/Writeups-CTF/blob/master/picoCTF2018/imagenes/vault5.png)

## What's My Name? - Points: 250

Este reto nos da un archivo .pcap que lo podemos abrir con [Wireshark](https://www.wireshark.org/) y en el hint nos dice "como nosotros sabemos el nombre del dominio?"

![alt text](https://github.com/richiprieto/Writeups-CTF/blob/master/picoCTF2018/imagenes/myname.png)
![alt text](https://github.com/richiprieto/Writeups-CTF/blob/master/picoCTF2018/imagenes/myname1.png)

Al abrir el archivo debemos hacer un filtro para conocer los dnsserver a los que se a comunicado  y encontramos nuestra flag

![alt text](https://github.com/richiprieto/Writeups-CTF/blob/master/picoCTF2018/imagenes/myname2.png)

## Safe RSA - Points: 250

Uno de los retos que personalmente más me gustó. Completar...
https://crypto.stackexchange.com/questions/33561/cube-root-attack-rsa-with-low-exponent
