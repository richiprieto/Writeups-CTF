- **Binwalk**
  - El nombre es muy explicito usamos binwalk para extraer los diferentes archivos que contiene la imagen proporcionada
  - ```binwalk -D=".*" PurpleThing.jpg``` 
  - Con eso obtenemos la flag en la carpeta que se creó
- **Forensics 101**
  - Nos dice si podemos extraer la imagen que se encuentra por ahi.
  - ```strings 95f6edfb66ef42d774a5a34581f19052.jpg | grep flag```
  - Obtenemos el flag
- **Basic Injection**
  - Su nombre lo indica debemos hacer una inyección SQL en la pagina web para extraer la DB
  - En mi caso usé BurpSuite, se captura el paquete y lo reenvias con el siguiente código de inyección
  - ```' or '1'='1```
  - El resultado es el dump de la base de datos con la flag
- **Character Encoding**
  - Observamos un código numérico en hexadecimal debido al uso de letras a-f
  - hay que trasladarlo a código ascii https://www.rapidtables.com/convert/number/hex-to-ascii.html
- **Hextroadinary**
  - En la descripción del reto hace una referencia a la operación de XOR y tenemos dos números en formato hex
  - ```0xc4115 xor 0x4cf8```
  - la operación se la puede realizar online https://toolslick.com/math/bitwise/xor-calculator
- **Simple Programming**
  - Nos pide que para todas cada una de las lineas si los valores de 0 son divisibles para 3 o los valores de 1 son divisibles para 2
  - ```python
    file = open("data.dat","r")
    counter = 0 
    for line in file:
      if line.count('0') % 3 == 0 or line.count('1') % 2 == 0:
        counter += 1
    print(counter)
    file.close()
    ```
   - Con eso obtenemos el número de lineas que es la flag
 - **Reykjavik**
    - Debemos hacer Ing. Inversa a un archivo, el que contendrá la flag
    - abrimos el archivo con gdb, se buscan las funciones ```info func```
    - desensamblamos la función main ```disas main```
    - como es un archivo corto podemos colocar un break en cualquier punto del main en lo personal me coloque en la instrucción ```je dirección 0x000055555555511b```
    - ```b \*0x000055555555511b```
    - y a partir de ahi ir recorriendo el programa linea a linea mediante steps ```s```
    - Veremos que a flag se encuentra en el stack
  - **Basic Android RE 1**
    - Como se indica se debe hacer una ingenieria inversa a una aplicación de android
    - Decompilamos el programa con http://www.javadecompilers.com/
    - Abrimos el archivo MainActivity.java
    - Vemos una función que valida la clave, dicha función compara la entrada con un valor que está en formato md5 por lo que se puede crackear mediante https://hashes.com/en/decrypt/hash
    - Una vez con este texto simplemente procedemos a hacer la unión que se encuentra en el código
    - ```CTFlearn{\<clavemd5crackeada\>_is_not_secure!}``` y listo
- **5x5 Crypto**
  - Nos habla de una criptografia en matriz 5x5 y nos pasa las direcciónes del código
  - Una rápida busqueda nos lleva a https://en.wikipedia.org/wiki/Tap_code
  - El reto se puede resolver manualmente, pero siempre es preferible escribir código
  - ```python
    cipher = [["A", "B", "C/K", "D", "E"],
         ["F", "G", "H", "I", "J"],
         ["L", "M", "N", "O", "P"],
         ["Q", "R", "S", "T", "U"],
         ["V", "W", "X", "Y", "Z"]]
    codigo = "1-3,4-4,2-1,{,4-4,2-3,4-5,3-2,1-2,4-3,_,4-5,3-5,}"
    codigo = codigo.split(",")
    flag = ''
    for value in codigo:
      if len(value) > 1:
        flag += cipher[int(value[0])-1][int(value[-1])-1]
      else:
        flag += value
    print(flag)
    ```
