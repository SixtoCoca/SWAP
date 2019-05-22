# Practica 5. Replicación de bases de datos MySQL
En esta práctica hay 4 objetivos:

1. Crear una BD con al menos una tabla y algunos datos.

2. Realizar la copia de seguridad de la BD completa usando mysqldump en la máquina principal y copiar el archivo de copia de seguridad a la máquina secundaria.

3. Restaurar dicha copia de seguridad en la segunda máquina (clonado manual de la BD), de forma que en ambas máquinas esté esa BD de forma idéntica.

4. Realizar la configuración maestro-esclavo de los servidores MySQL para que la replicación de datos se realice automáticamente.

---

Creamos la base de datos con algunos datos siguiendo el guion:
	
	mysql> create database contactos;
	mysql> use contactos;
	mysql> show tables;
	mysql> create table datos(nombre varchar(100),tlf int);
	mysql> insert into datos(nombre,tlf) values ("pepe",95834987);

Quedando la base de datos asi:

![img](https://github.com/SixtoCoca/SWAP/blob/master/Imagenes/basededatos.png)

## Replicar una BD usando mysqldump

Primero bloqueamos la base de datos para que no se actualize:

	mysql> FLUSH TABLES WITH READ LOCK;

Luego utilizamos mysqldump para guardar los datos:

	mysqldump contactos -u root -p > /tmp/contactos.sql

Luego desbloqueamos las tablas:

	mysql> UNLOCK TABLES;

En la maquina 2 copiamos el archivo .sql con tos uss datos guardados en la máquina 1.

	scp 192.168.1.10:/tmp/contactos.sql /tmp/

![img](https://github.com/SixtoCoca/SWAP/blob/master/Imagenes/scriptiptables.png)

Para que este script se ejecute cada vez que se arranca la maquina(y por tanto tengamos el cortafuegos siempre activo) añadimos lo siguiente en el fichero /etc/rc.local

![img](https://github.com/SixtoCoca/SWAP/blob/master/Imagenes/rc.local.png)

Con esto ya podemos ver que nos funciona el cortafuegos en la maquina instalada.

![img](https://github.com/SixtoCoca/SWAP/blob/master/Imagenes/iptablesm1.png)
