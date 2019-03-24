# Practica 1. Preparación de las herramientas

En esta práctica hay 2 objetivos:

1. acceder por ssh de una máquina a otra

2. acceder mediante la herramienta curl desde una máquina a la otra

---

En primer lugar he instalado 2 maquinas virtuales ubuntuserver16 con Apache+PHP+MySQL

Una vez instaladas he tenido que crear en VirtualBox una red solo-anfitrion para que se puedan
conectar entre ellas.

![img](https://github.com/SixtoCoca/SWAP/blob/master/Imagenes/redvirtualbox.png)

Modificamos el archivo /etc/network/interfaces añadiendo lo siguiente(en ambas maquinas virtuales cambiando en cada uno el parámetro addres)

![img](https://github.com/SixtoCoca/SWAP/blob/master/Imagenes/capturaip.png)

Una vez hecho esto ya esta listo nuestras maquinas para poder acceder una otra usando ssh o utilizando cURL.

Comprobamos que ya funciona el ssh:

![img](https://github.com/SixtoCoca/SWAP/blob/master/Imagenes/ssh.png)

Comprobamos que funciona el cURL:

![img](https://github.com/SixtoCoca/SWAP/blob/master/Imagenes/curl.png)