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

![img](https://github.com/SixtoCoca/SWAP/blob/master/Imagenes/contactosscp.png)

## Replicar una BD mediante una configuración maestro-esclavo

Comprobamos que tienen la mismas version las maquinas virtuales.

Añadimos esta configuración en el archivo /etc/mysql/mysql.conf.d/mysqld.cnf:

	#bind-address 127.0.0.1
	log_error = /var/log/mysql/error.log
	server-id = 1
	log_bin = /var/log/mysql/bin.log

Reiniciamos el servicio. Configuramos el esclavo poniendo server-id=2 y reiniciamos el servicio esclavo.

Creamos un usuario y le damos permiso para replicar en la maquina maestra:

	mysql> CREATE USER esclavo IDENTIFIED BY 'esclavo';
	mysql> GRANT REPLICATION SLAVE ON *.* TO 'esclavo'@'%'
	IDENTIFIED BY 'esclavo';
	mysql> FLUSH PRIVILEGES;	
	mysql> FLUSH TABLES;
	mysql> FLUSH TABLES WITH READ LOCK;

Mostrando el show master status:

![img](https://github.com/SixtoCoca/SWAP/blob/master/Imagenes/showmasterstatus.png)

En la maquina esclava introducimos los datos del maestro vistos en show master status:

	mysql> CHANGE MASTER TO MASTER_HOST='192.168.1.10',
	MASTER_USER='esclavo', MASTER_PASSWORD='esclavo',
	MASTER_LOG_FILE='bin.000001', MASTER_LOG_POS=154,
	MASTER_PORT=3306;

![img](https://github.com/SixtoCoca/SWAP/blob/master/Imagenes/ESCLAVO.png)

Arrancamos el esclavo utilizando y desbloqueamos las tablas:

	mysql> START SLAVE;
	mysql> UNLOCK TABLES

Vemos el SHOW SLAVE STATUS(vemos que la variable Seconds_Behind_Master esta a 0):

![img](https://github.com/SixtoCoca/SWAP/blob/master/Imagenes/secondbehindmaster.png)

Aqui vemos como se replica:

![img](https://github.com/SixtoCoca/SWAP/blob/master/Imagenes/solucionfinal.png)
